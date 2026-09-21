# 📖 对照翻译：Document Service API: Middlewares

> Source: `docusaurus/docs/cms/api/document-service/middlewares.md`  
> Upstream SHA: `5500469d36bd416a09e2d69918df62ca4be4b041`

**Original:** Document Service middlewares allow you to perform actions before and after Document Service methods run by registering middleware functions via `strapi.documents.use()` with access to content type context and method parameters.

**中文译文:** Document Service middlewares 可以在 Document Service method 执行前后插入自定义逻辑。通过 `strapi.documents.use()` 注册 middleware function 后，可以访问 content type context、当前 action 以及 method parameters。

**Original:** The Document Service API can be extended through middlewares. Middlewares can perform actions before and/or after a method runs.

**中文译文:** Document Service API 支持通过 middleware 扩展行为。Middleware 可以在 method 执行之前处理 parameters，也可以在执行之后处理 result。

## Registering a middleware

**Original:** Syntax: `strapi.documents.use(middleware)`

**中文译文:** 注册语法：

`strapi.documents.use(middleware)`

**Original:** A middleware receives `context` and `next`.

`(context, next) => ReturnType<typeof next>`

**中文译文:** Middleware function 接收两个参数：`context` 与 `next`，返回值应与 `next()` 的返回类型一致。

| Parameter | 中文说明 | Type |
|---|---|---|
| `context` | 当前 Document Service middleware context | `Context` |
| `next` | 调用 middleware stack 中的下一个 middleware | function |

### `context`

**Original:**

| Parameter | Description |
|---|---|
| `action` | Method currently running |
| `params` | Method parameters |
| `uid` | Content type UID |
| `contentType` | Content type definition |

**中文译文:**

| Parameter | 中文说明 |
|---|---|
| `action` | 当前执行的 Document Service method，例如 `findOne`、`findMany`、`create`、`update`、`delete` |
| `params` | 当前 method 的 parameters |
| `uid` | Content type unique identifier，例如 `api::restaurant.restaurant` |
| `contentType` | 完整 content type definition |

**Original:** The exact `params` depend on the action. A `findOne` context can include `documentId`, `locale`, `status`, and `populate`; `findMany` can include `filters`, `status`, `locale`, and `fields`; create/update/delete include their corresponding data and identifiers.

**中文译文:** `params` 的结构取决于当前 action。例如：
- `findOne` 可能包含 `documentId`、`locale`、`status`、`populate`；
- `findMany` 可能包含 `filters`、`status`、`locale`、`fields`；
- `create`、`update`、`delete` 则包含各自需要的 `data`、identifier、locale 或 population options。

### `next`

**Original:** `next` is a function without parameters that calls the next middleware in the stack and returns its response.

```js
strapi.documents.use((context, next) => {
  return next();
});
```

**中文译文:** `next()` 不接收参数，用于调用 middleware stack 中的下一个 middleware，并返回后续执行结果。最基本的 pass-through middleware 如上，代码保持原样。

## Where to register

**Original:** Generally, middlewares should be registered during Strapi's registration phase.

**中文译文:** 通常应在 Strapi 的 **registration phase** 注册 Document Service middleware，而不是等到 bootstrap 后再注册。

### Users

**Original:** Register middleware in the application's `register()` lifecycle:

```js title="/src/index.js|ts"
module.exports = {
  register({ strapi }) {
    strapi.documents.use((context, next) => {
      // your logic
      return next();
    });
  },
};
```

**中文译文:** 普通 Strapi application 可以在根 `/src/index.js|ts` 的 `register()` lifecycle 中调用 `strapi.documents.use()`。代码保持原样。

### Plugin developers

**Original:** Register middleware in the plugin's `register()` lifecycle:

```js title="/(plugin-root-folder)/strapi-server.js|ts"
module.exports = {
  register({ strapi }) {
    strapi.documents.use((context, next) => {
      // your logic
      return next();
    });
  },
};
```

**中文译文:** Plugin developer 应在 plugin 自己的 `register()` lifecycle 中注册 middleware。

## Implementing a middleware

**Original:** Always return the response from `next()`. Failing to do this breaks the Strapi application.

**中文译文:** 实现 middleware 时必须始终返回 `next()` 的 response。如果调用后不 return，可能破坏整个 Strapi application 的 Document Service 调用链。

**Original:**
```js
const applyTo = ['api::article.article'];

strapi.documents.use(async (context, next) => {
  if (!applyTo.includes(context.uid)) {
    return next();
  }

  if (['create', 'update'].includes(context.action)) {
    context.params.data.fullName =
      `${context.params.data.firstName} ${context.params.data.lastName}`;
  }

  const result = await next();

  return result;
});
```

**中文译文:** 上例只对 `api::article.article` 生效，并且只在 `create` / `update` 时，根据 `firstName` 与 `lastName` 自动写入 `fullName`。随后调用并返回 `next()` 的执行结果。代码中的 identifiers 保持原样。

**Original:** Document Service API methods also trigger database lifecycle hooks. See the lifecycle-hooks reference for details.

**中文译文:** Document Service API method 还会触发相应 database lifecycle hooks。完整对应关系请参阅 [Document Service API: Lifecycle hooks](/cms/migration/v4-to-v5/breaking-changes/lifecycle-hooks-document-service#table)。
