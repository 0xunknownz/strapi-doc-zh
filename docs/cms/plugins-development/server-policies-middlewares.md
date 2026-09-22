# 📖 对照翻译：Server API — Policies & Middlewares

> Source: `docusaurus/docs/cms/plugins-development/server-policies-middlewares.md`  
> Upstream SHA: `8ac70b6f98e39f525d77e5bfc08556091b6f2e8b`

**Original:** Policies decide whether a request can proceed. Middlewares shape how a request is processed.

**中文译文:** Plugin server 中：
- **Policy**：决定 request 是否允许继续；
- **Middleware**：在 request / response lifecycle 周围执行逻辑、修改 context 或 response。

## Decision guide

| 需求 | 推荐机制 |
|---|---|
| 按 user role/state 拒绝 request | Policy |
| 按 body/header 做 access check | Policy |
| 不满足条件返回 403 | Policy |
| 多 routes 共享访问规则 | Named policy |
| 给 plugin routes 增加 header / query normalization | Route middleware |
| 对整个 Strapi server 做 tracing/logging | Server-level middleware |
| 修改 `ctx.query` 后再进 controller | Route middleware |

## Policies

**Original:** A policy runs before the controller. Return `true` to allow, `false` to block.

**中文译文:** Policy 在 controller 之前运行。Function 接收：
- `policyContext`：对 Koa context 的 policy wrapper；
- `config`：route 中该 policy 的 `options`；
- `{ strapi }`。

**Original code (kept unchanged):**

```js
module.exports = (
  policyContext,
  config,
  { strapi }
) => {
  const { user } = policyContext.state;
  const targetRole = config.role;

  if (!user || !targetRole) {
    return false;
  }

  const roles = Array.isArray(user.roles)
    ? user.roles
    : user.role
      ? [user.role]
      : [];

  return roles.some((role) => {
    if (typeof role === 'string') {
      return role === targetRole;
    }

    return (
      role?.code === targetRole ||
      role?.name === targetRole
    );
  });
};
```

**中文译文:** 示例兼容 `user.role` 与 `user.roles` 两种 authentication context shape，并根据 route-provided role option 做判断。

### Route usage

```js
config: {
  policies: [
    'plugin::my-plugin.isActive',
    {
      name: 'plugin::my-plugin.hasRole',
      options: {
        role: 'editor',
      },
    },
    (policyContext, config, { strapi }) => true,
  ],
}
```

**Original:** Returning `undefined` is permissive, not blocking.

**中文译文:** **重要：Policy 没有 return（`undefined`）会被视为允许 request。** 如果想阻止必须明确 `return false`，或抛出 Strapi HTTP error。

**Original:** Throwing a plain Error produces 500; use `PolicyError`, `ForbiddenError`, or `UnauthorizedError` for intentional HTTP errors.

**中文译文:** 普通 `throw new Error()` 会产生 500。预期的访问控制错误应使用 Strapi 的 `PolicyError`、`ForbiddenError`、`UnauthorizedError` 等。

## Route-level middlewares

**Original:** Plugin route middleware uses a two-level factory signature.

**中文译文:** Named route middleware 是**双层 factory**：

```js
module.exports =
  (config, { strapi }) =>
  async (ctx, next) => {
    strapi.log.info(
      `[my-plugin] ${ctx.method} ${ctx.url}`
    );

    await next();

    strapi.log.info(
      `[my-plugin] → ${ctx.status}`
    );
  };
```

**中文译文:** Outer function 接收 route middleware options 与 Strapi instance；inner function 才是实际每次 request 调用的 Koa middleware。

### Route declaration

```js
config: {
  middlewares: [
    'plugin::my-plugin.logRequest',
    async (ctx, next) => {
      ctx.query.pageSize =
        ctx.query.pageSize || '10';

      await next();
    },
  ],
}
```

**中文译文:** Named middleware 可复用；inline middleware 适合简单、单 route 逻辑。

## Server-level middlewares

**Original:** Register on the global HTTP server with `strapi.server.use()` in `register()`.

```js
module.exports = ({ strapi }) => {
  strapi.server.use(async (ctx, next) => {
    const start = Date.now();

    await next();

    const ms = Date.now() - start;

    ctx.set(
      'X-Response-Time',
      `${ms}ms`
    );
  });
};
```

**中文译文:** Server-level middleware 会影响**整个 Strapi server 的所有 routes**，不只 plugin endpoint。只针对 plugin 的需求应优先使用 route middleware。

**Original:** A server-level middleware that throws or never calls `next()` can break all requests.

**中文译文:** Global middleware 如果抛错或忘记 `await next()`，可能让整个 application request chain 中断。

## Best practices

**中文译文:**
- Policy 第一参数叫 `policyContext`，不要把它误当原始 `ctx`；
- Policy 始终显式返回 `true` / `false`；
- Middleware 尽量 route-scoped；
- Koa middleware 需要继续下游时必须 `await next()`；
- 同一个 policy 在多个 routes 使用不同参数时，用 `{ name, options }` 复用。
