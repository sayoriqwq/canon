---
title: "Effect Without Effect-TS: Algebraic Thinking in Plain TypeScript"
url: "https://cekrem.github.io/posts/effect-without-effect-ts/"
author:
  - "Christian Ekrem"
published: 2026-04-14
description: "The ideas behind Effect-TS are 40 years old. You can use most of them today, in plain TypeScript, without adopting a framework."
authority:
note:
---
A lot of people are reaching for [Effect-TS](https://effect.website/).  
很多人都在寻找 [Effect-TS](https://effect.website/) 。

Every few months you’ll be three functions deep in some TypeScript service, squinting at a `try/catch` that swallows four different kinds of failure into one `catch (err)`, and you’ll think: “Effect would fix this.” Then you look at the API surface, the generator syntax, the layers and services and fibers, and you quietly close the tab. Not because it’s bad (not at all; it’s genuinely impressive software.) But it requires some investment, and you’re just not quite sure…  
每隔几个月，你就会陷入某个 TypeScript 服务中三个函数的深度，眯着眼睛盯着一个 `try/catch` ，它把四种不同的错误都吞进了一个 `catch (err)` 里，然后你会想：“Effect 就能解决这个问题。” 然后你仔细查看了 API 接口、生成器语法、层级结构、服务和纤程，最后默默地关掉了网页。倒不是因为它不好（完全不是；它确实是令人印象深刻的软件。）而是因为它需要投入一些时间和精力，而你对此还不太确定……

But what if the *ideas* behind it don’t require the framework, and you can use most of them with what TypeScript gives you out of the box?  
但是，如果背后的 *理念* 并不需要框架，而且你可以使用 TypeScript 开箱即用的功能来实现其中的大部分呢？

If you read my [parse-don’t-validate post](https://cekrem.github.io/posts/parse-dont-validate-typescript/), you already used one of those ideas. The `Parsed<T>` type that returns either a value or an error? That’s typed errors as values. You were doing algebraic thinking without knowing it. (I was too, for years, before I learned what to call it.)  
如果你读过我 [那篇关于“解析而不验证”的文章](https://cekrem.github.io/posts/parse-dont-validate-typescript/) ，那你已经用到其中的一个思路了。返回值或错误的 `Parsed<T>` 类型？那就是把类型错误当作值来处理。你之前一直在用代数思维，只是自己没意识到而已。（我也一样，好多年都没意识到。）

This post takes that thread and pulls it further. Same principle (“make the type system carry the proof”) applied to operations instead of data.  
这篇文章延续了之前的思路，并将其进一步延伸。同样的原则（“让类型系统承载证明”）被应用于操作而非数据。

## The function that lies to you 欺骗你的功能

Here’s a signup function we’ve written in some form at, well, every company we’ve worked at:  
以下是我们几乎在所有工作过的公司都编写过的注册功能：

```typescript
async function signupUser(email: string, password: string): Promise<User> {
  if (!isValidEmail(email)) {
    throw new Error("Invalid email");
  }

  const existing = await db.findUserByEmail(email);
  if (existing) {
    throw new Error("Email already registered");
  }

  const user = await db.createUser({
    email,
    passwordHash: await hash(password),
  });

  await emailService.sendWelcome(user.email);
  await analytics.track("user_signed_up", { userId: user.id });

  return user;
}
```

The return type says `Promise<User>`. That’s a lie. This function can fail in at least four ways (bad email, duplicate, database down, email service timeout), calls a database, sends an email, tracks analytics. None of that is in the signature. The caller has to wrap it in `try/catch` and guess:  
返回类型显示为 `Promise<User>` ，这是个谎言。这个函数至少有四种可能失败的情况（邮箱地址错误、重复、数据库宕机、邮件服务超时），它会调用数据库、发送邮件、跟踪分析数据。但这些都没有在函数签名中明确说明。调用者必须使用 `try/catch` 包裹函数并进行猜测。

```typescript
try {
  const user = await signupUser(email, password);
  res.json({ ok: true, user });
} catch (err) {
  // What kind of error? Validation? DB? Email service?
  // No idea. The type system forgot.
  res.status(400).json({ error: (err as Error).message });
}
```

Same problem as [the parse-don’t-validate post](https://cekrem.github.io/posts/parse-dont-validate-typescript/), one level up. A `string` pretending to be an email was a lie. A `Promise<User>` pretending to always succeed is the same lie.  
和 [“解析不验证”那篇文章的](https://cekrem.github.io/posts/parse-dont-validate-typescript/) 问题一样，只是程度不同。一个伪装成电子邮件地址的 `string` 是谎言。一个伪装成永远成功的 `Promise<User>` 也是同样的谎言。

## Idea 1: honest errors 想法一：诚实的错误

You know this part from the parse-don’t-validate post, so I’ll go fast.  
你已经从那篇关于 parse-don't-validate 的文章中了解了这部分内容，所以我快速讲解一下。

Instead of throwing, return the error as a value. Make each failure a variant in a discriminated union:  
不要抛出错误，而是将错误作为值返回。将每次失败都作为可区分联合体中的一个变体：

```typescript
type SignupError =
  | { _tag: "InvalidEmail" }
  | { _tag: "EmailTaken"; email: string }
  | { _tag: "DbError"; cause: unknown }
  | { _tag: "EmailServiceDown" };

type Result<T, E> = { ok: true; value: T } | { ok: false; error: E };
```

(I’m using `_tag` instead of `kind` here – convention I picked up from the Effect community, and it avoids collisions with domain fields named `kind`. Use whatever you want, property name is not the point.)  
（这里我用的是 `_tag` 而不是 `kind` 这是我从 Effect 社区学来的约定，这样可以避免与名为 `kind` 域字段冲突。你可以随意使用，属性名并不重要。）

Now the signup function returns `Promise<Result<User, SignupError>>`. The caller switches on `error._tag` and the compiler checks exhaustiveness – *if* you add the `assertNever` trick:  
现在注册函数返回 `Promise<Result<User, SignupError>>` 。调用者会启用 `error._tag` ，编译器会检查穷尽性—— *如果* 您添加了 `assertNever` 技巧：

```typescript
function assertNever(x: never): never {
  throw new Error(\`Unexpected: ${JSON.stringify(x)}\`);
}

// at the call site:
if (!result.ok) {
  switch (result.error._tag) {
    case "InvalidEmail":
      return res.status(400).json({ error: "Bad email" });
    case "EmailTaken":
      return res.status(409).json({ error: "Already registered" });
    case "DbError":
      return res.status(500).json({ error: "Try again later" });
    case "EmailServiceDown":
      return res
        .status(202)
        .json({ message: "Signed up, welcome email delayed" });
    default:
      assertNever(result.error);
  }
}
```

Add a fifth error variant next month and the compiler flags every `switch` that doesn’t handle it. In Elm this would just be a compile error you can’t ignore. In TypeScript you need the `assertNever` dance, which is less elegant but does the job.  
下个月新增第五种错误类型后，编译器会标记所有未处理该错误的 `switch` 语句。在 Elm 中，这会直接导致编译错误，无法忽略。而在 TypeScript 中，你需要使用 `assertNever` 语句，虽然不够优雅，但也能解决问题。

One thing that might bite you, though: TypeScript sometimes infers `string` instead of the literal `"InvalidEmail"` for `_tag`. If that happens, use constructor functions:  
不过，有一点需要注意：TypeScript 有时会将 `_tag` 推断为 `string` 而不是字面值 `"InvalidEmail"` 。如果发生这种情况，请使用构造函数：

```typescript
const invalidEmail = (): SignupError => ({ _tag: "InvalidEmail" });
const emailTaken = (email: string): SignupError => ({
  _tag: "EmailTaken",
  email,
});
```

Or just `as const` the object. Either way, you need the literal types for narrowing to work.  
或者直接 `as const` 对象。无论哪种方式，都需要字面类型才能使类型缩小生效。

This is idea 1, and you’ve already been doing it if you followed the parse-don’t-validate series. The new part starts now. Lo and behold:  
这是第一种方法，如果你一直关注“解析但不验证”系列教程，那么你已经在实践这种方法了。现在，新的部分开始了。瞧！

## Idea 2: honest dependencies想法二：诚实的依赖关系

The return type of our signup function is now `Promise<Result<User, SignupError>>`. Better – the error channel is visible. But the function still secretly depends on a database, an email service, and an analytics client, all hiding behind module-level imports. The function’s *real* inputs aren’t just `email` and `password`. They’re also “a database that’s up” and “an email service that works.” The type signature doesn’t mention any of them.  
我们的注册函数的返回类型现在是 `Promise<Result<User, SignupError>>` 。这样好多了——错误通道现在可见了。但该函数仍然暗中依赖于数据库、邮件服务和分析客户端，所有这些都隐藏在模块级导入之后。该函数的 *真正* 输入不仅仅是 `email` 和 `password` ，还包括“一个正常运行的数据库”和“一个正常工作的邮件服务”。类型签名中并没有提及这些。

In [Why TypeScript Won’t Save You](https://cekrem.github.io/posts/why-typescript-wont-save-you/), I talked about the gap between what the type system sees and what actually happens at runtime. Hidden dependencies live in exactly that gap.  
在 [《为什么 TypeScript 救不了你》](https://cekrem.github.io/posts/why-typescript-wont-save-you/) 一文中，我讨论了类型系统所看到的和运行时实际发生的情况之间的差距。隐藏依赖项就存在于这个差距之中。

The fix is the simplest idea in this whole post, and I almost feel dumb writing it out: put the dependencies in the function signature.  
解决方法是这篇文章中最简单的，我写出来都觉得有点傻：把依赖项放在函数签名里。

```typescript
type SignupDeps = {
  readonly findUserByEmail: (
    email: string,
  ) => Promise<Result<User | null, DbError>>;
  readonly createUser: (
    input: CreateUserInput,
  ) => Promise<Result<User, DbError>>;
  readonly sendWelcomeEmail: (
    email: string,
  ) => Promise<Result<void, EmailError>>;
  readonly trackEvent: (
    name: string,
    props: Record<string, string>,
  ) => Promise<void>;
};
```

Now the function takes its dependencies as the first argument:  
现在该函数将它的依赖项作为第一个参数：

```typescript
async function signupUser(
  deps: SignupDeps,
  email: string,
  password: string,
): Promise<Result<User, SignupError>> {
  const parsed = parseEmail(email);
  if (!parsed.ok) return { ok: false, error: { _tag: "InvalidEmail" } };

  const existing = await deps.findUserByEmail(parsed.value);
  if (!existing.ok)
    return { ok: false, error: { _tag: "DbError", cause: existing.error } };
  if (existing.value)
    return { ok: false, error: { _tag: "EmailTaken", email } };

  const created = await deps.createUser({
    email: parsed.value,
    passwordHash: await hash(password),
  });
  if (!created.ok)
    return { ok: false, error: { _tag: "DbError", cause: created.error } };

  const welcomed = await deps.sendWelcomeEmail(parsed.value);
  if (!welcomed.ok) {
    // Non-fatal: user is created, email just didn't send
    // (log it, retry later, whatever)
  }

  await deps.trackEvent("user_signed_up", { userId: created.value.id });

  return { ok: true, value: created.value };
}
```

Read the signature: `signupUser(deps: SignupDeps, email: string, password: string): Promise<Result<User, SignupError>>`. That’s the whole story. What it needs, what it takes, what it returns, how it can fail. No ambient imports, no hidden capabilities. If you read that line and nothing else, you know what this function does.

(If you’ve read Scott Wlaschin’s *Domain Modeling Made Functional*, you’ll recognize this – he passes dependencies as function parameters and then partially applies them. In F# the currying makes it natural. In TypeScript it’s a bit more explicit, but the principle is identical. You could use lodash functional or rambda or something to support currying, btw.)

The payoff shows up immediately in tests:

```typescript
const fakeUser: User = { id: "1", email: "test@example.com" };

const result = await signupUser(
  {
    findUserByEmail: async () => ({ ok: true, value: null }),
    createUser: async () => ({ ok: true, value: fakeUser }),
    sendWelcomeEmail: async () => ({ ok: true, value: undefined }),
    trackEvent: async () => {},
  },
  "test@example.com",
  "password123",
);

expect(result).toEqual({ ok: true, value: fakeUser });
```

No mocking library needed! And no `jest.spyOn(db, 'findUserByEmail')`. Just… functions. The dependencies are in the type, so TypeScript tells you exactly what to provide. If you forget one, it’s a compile *error*, not a runtime “what happened now, and what does that exception really mean?”.

And in production, you wire it (once!) at the edge:

```typescript
const prodDeps: SignupDeps = {
  findUserByEmail: postgresUserRepo.findByEmail,
  createUser: postgresUserRepo.create,
  sendWelcomeEmail: sendgridClient.sendWelcome,
  trackEvent: segmentClient.track,
};

router.post("/signup", async (req, res) => {
  const result = await signupUser(prodDeps, req.body.email, req.body.password);
  // handle result...
});
```

This is dependency injection, without all the `@Injectable()`. We usually use tools (not just Effect) to handle much of this, but it’s a good thing to at least know how to do it without all the magic tricks! Just a type and a function parameter. The “infrastructure layer” from [Clean Architecture](https://cekrem.github.io/posts/clean-architecture-and-plugins-in-go/) is literally just the `prodDeps` object.

I already covered this pattern in Elm and F# in [the impossible-states post](https://cekrem.github.io/posts/making-impossible-states-impossible-with-functional-dependency-injection/). Turns out it works fine in TypeScript too, it’s just more verbose (and way less common!).

## Idea 3: composition (and where it gets ugly)

Look at the `signupUser` body again. See all those early returns?

```typescript
const existing = await deps.findUserByEmail(parsed.value);
if (!existing.ok) return { ok: false, error: { _tag: "DbError", cause: existing.error } };

const created = await deps.createUser({ ... });
if (!created.ok) return { ok: false, error: { _tag: "DbError", cause: created.error } };

const welcomed = await deps.sendWelcomeEmail(parsed.value);
if (!welcomed.ok) { ... }
```

If you read the parse-don’t-validate post, you’ve seen this before – the `parseUser` function had the same shape. Check result, bail on error, continue on success, repeat. It works. It’s also six lines of plumbing for every two lines of logic.

You can clean this up with a small helper:

```typescript
async function andThen<T, U, E1, E2>(
  result: Promise<Result<T, E1>>,
  f: (value: T) => Promise<Result<U, E2>>,
): Promise<Result<U, E1 | E2>> {
  const r = await result;
  if (!r.ok) return r;
  return f(r.value);
}
```

This is `flatMap` for async results. If the previous step failed, skip everything. If it succeeded, run the next step. The error types union automatically. (In F# this would be `Result.bind` inside an `async` computation expression. In Elm it’s `Result.andThen`. Same idea, different syntax.)

And if you must know, by doing this, you’re not far from making a [Monad](https://cekrem.github.io/posts/functors-applicatives-monads-elm/#monad-i-have-a-wrapped-value-and-a-function-that-returns-a-wrapped-value), though that scary term doesn’t necessarily help us at this point.

For two or three steps, `andThen` cleans things up nicely. Past four or five, the nesting gets painful. You start wishing for something like F#’s computation expressions or Haskell’s `do` notation – a way to write what looks like straight-line code but with the error handling baked in.

And that is, quite honestly, where Effect-TS earns its weight. Its generator-based syntax gives you exactly that:

```typescript
// Effect-TS version (for comparison, not what we're building)
const signupUser = Effect.gen(function* () {
  const email = yield* parseEmail(rawEmail);
  const existing = yield* deps.findUserByEmail(email);
  // ... looks like straight-line code, but errors propagate automatically
});
```

I’m not going to build that in this post. If I started writing combinators on top of combinators I’d end up with a worse version of Effect, and that’s not the point.

## Where this breaks down

I want to be honest about the limits, because overselling this stuff is how you end up writing [FP articles you can’t finish](https://cekrem.github.io/posts/the-fp-article-i-cant-seem-to-finish/).

Result composition past four or five steps gets verbose. The early-return pattern works, it’s just a lot of characters for not much meaning. The `andThen` helper takes the edge off but introduces nesting. Past a certain point you’re fighting the language. TypeScript doesn’t have `do` notation and probably never will.

Error types also multiply across module boundaries. When `signupUser` calls `createOrder` which calls `chargePayment`, each layer has its own error union. You end up manually merging them or writing mapping functions between layers. Fine for two levels. Annoying at five.

And structured concurrency is a different game entirely. “Run these three things in parallel, cancel the rest if one fails, make sure cleanup happens” – `Promise.allSettled` gives you nothing type-safe. Effect’s fiber model is genuinely better here, and I’m not going to pretend otherwise.

These are real limits. The patterns in this post cover maybe 80% of what I need day-to-day. The other 20% is where I keep almost reaching for Effect.

In any case, I’ll argue *it’s often good to learn to do manually even things a framework can do better automagically*. Often.

## What this actually is

Typed errors are a 10-line `Result` type. Explicit effects are `Promise<Result<T, E>>` instead of `Promise<T>`. Dependency injection is a function parameter. None of this requires a library. You can adopt typed errors tomorrow without touching your DI story. You can inject dependencies without a single `Result` type. They work independently, and they compound when you combine them.

Effect-TS packages all of these (and more) into a coherent system with good ergonomics. That’s worth something. But the ideas predate it by decades, and they come from the same tradition as parse-don’t-validate.

Reaching for Effect makes sense. But when you choose to go all in that route, I hope you know *why* it exists – and that’s (IMHO) worth more than the library. `¯\_(ツ)_/¯`