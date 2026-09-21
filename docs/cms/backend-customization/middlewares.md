# 📖 对照翻译：Middlewares customization

> Source: `docusaurus/docs/cms/backend-customization/middlewares.md`  
> Upstream SHA: `b5f9c5953f7608bb3ddcbbadc6afd0cb93c49296`

**Original:** Middlewares alter the request or response flow at application or API levels. This documentation distinguishes global versus route middlewares and illustrates custom implementations.

**中文译文:** Middlewares 用于修改 request / response flow，可以作用于 application level 或 API level。本页重点介绍 custom global / API middleware 的实现，并说明与 route middleware、Document Service middleware 的区别。

**Original:** A new application-level or API-level middleware can be generated with `strapi generate` or created manually.

**中文译文:** 新 middleware 可以：
- 通过 interactive CLI `strapi generate` 创建；
- 或手动创建文件。

**Original:** Locations:
- `./src/middlewares/` application-level
- `./src/api/[api-name]/middlewares/` API-level
- `./src/plugins/[plugin-name]/middlewares/` plugin middleware

**中文译文:** 文件位置：
- `./src/middlewares/`：application-level；
- `./src/api/[api-name]/middlewares/`：API-level；
- `./src/plugins/[plugin-name]/middlewares/`：plugin middleware。

**Original code (kept unchanged):**

```js
module.exports = (config, { strapi }) => {
  return (context, next) => {};
};
```

```ts
export default (config, { strapi }) => {
  return (context, next) => {};
};
```

**中文译文:** REST middleware factory 接收 middleware `config` 与 Strapi context，并返回实际处理 `context`、`next` 的 function。

**Original:** Globally scoped middlewares must be added to the middlewares configuration file or Strapi will not load them.

**中文译文:** Application-wide global middleware 必须加入 [middlewares configuration](/cms/configurations/middlewares#loading-order)，否则 Strapi 不会加载。

**Original:** API/plugin middlewares can be configured in routers.

```js
module.exports = {
  routes: [
    {
      method: "GET",
      path: "/[collection-name]",
      handler: "[controller].find",
      config: {
        middlewares: ["[middleware-name]"],
      },
    },
  ],
};
```

**中文译文:** API / plugin middleware 通常绑定到具体 route，在 route `config.middlewares` 中声明。

### Timer middleware example

```js
module.exports = () => {
  return async (ctx, next) => {
    const start = Date.now();

    await next();

    const delta = Math.ceil(Date.now() - start);
    ctx.set('X-Response-Time', delta + 'ms');
  };
};
```

**中文译文:** 示例在 `await next()` 之前记录时间，在下游处理完成后计算 response time，并写入 `X-Response-Time` header。这体现了 Koa middleware 的“洋葱模型”。

**Original:** GraphQL custom middleware uses a different syntax.

**中文译文:** GraphQL plugin 也支持 custom middleware，但 syntax 与 REST middleware 不同，应参阅 GraphQL customization 文档。

**Original:** Use `yarn strapi middlewares:list` to list registered middlewares.

**中文译文:** 可运行 `yarn strapi middlewares:list` 查看当前注册的全部 middlewares，便于确认 naming 与 router wiring。

## Usage and naming

**Original:**
- `global::middleware-name` for application-level
- `api::api-name.middleware-name` for API-level
- `plugin::plugin-name.middleware-name` for plugin middlewares

**中文译文:** 在 route config 中引用 middleware 时使用：
- application-level：`global::middleware-name`；
- API-level：`api::api-name.middleware-name`；
- plugin：`plugin::plugin-name.middleware-name`。

## "is-owner" middleware

**Original:** A common requirement is allowing only an entry author to edit/delete it. In Strapi v4+, middleware is the recommended mechanism.

**中文译文:** 常见业务需求是“只有 entry author 可以 edit / delete 自己的内容”。Strapi 4+ 推荐通过 middleware 实现这类 is-owner 逻辑。

**Original:** Generate an API middleware, load the current user and entry, compare owner IDs, and either call `next()` or return unauthorized.

**中文译文:** 基本实现流程：
1. 使用 `strapi generate` 创建 API middleware，例如 `isOwner`；
2. 从 `ctx.state.user` 获取当前 authenticated user；
3. 根据 request identifier 查询目标 entry，并 populate author relation；
4. 比较 user id 与 entry author id；
5. 相同则 `return next()`，否则 `ctx.unauthorized()`。

**Original example (adapted code kept unchanged in identifiers):**

```js
module.exports = (config, { strapi }) => {
  return async (ctx, next) => {
    const user = ctx.state.user;
    const entryId = ctx.params.id ? ctx.params.id : undefined;
    let entry = {};

    if (entryId) {
      entry = await strapi.documents('api::restaurant.restaurant').findOne(
        entryId,
        { populate: "*" }
      );
    }

    if (user.id !== entry.author.id) {
      return ctx.unauthorized("This action is unauthorized.");
    } else {
      return next();
    }
  };
};
```

**中文译文:** 核心逻辑如上。实际 Strapi 5 项目应根据当前 route identifier / Document Service signature 调整 entry lookup。

**Original:** Bind the middleware only to update/delete routes if read/create should remain available to others.

```js
const { createCoreRouter } = require("@strapi/strapi").factories;

module.exports = createCoreRouter("api::restaurant.restaurant", {
  config: {
    update: {
      middlewares: ["api::restaurant.is-owner"],
    },
    delete: {
      middlewares: ["api::restaurant.is-owner"],
    },
  },
});
```

**中文译文:** 上例只在 `update` 与 `delete` actions 上绑定 `is-owner`，因此 GET / create 等 route 不受该 middleware 限制。

**Original:** Route-level middleware is also useful for centralizing population logic and preventing over-fetching.

**中文译文:** Route middleware 也适合集中处理 population、query normalization、rate / access logic，从而减少重复代码与 accidental over-fetching。
