# 📖 对照翻译：Controllers

> Source: `docusaurus/docs/cms/backend-customization/controllers.md`  
> Upstream SHA: `38fee4d85abb59760e983103fb0aeaf8819af7a5`

**Original:** Controllers bundle actions that handle business logic for each route within Strapi's MVC pattern. This documentation demonstrates generating controllers, extending core ones with `createCoreController`, and delegating heavy logic to services.

**中文译文:** Controller 是 Strapi MVC 中负责处理 route action 的业务入口。它接收 `ctx`，执行或编排业务逻辑，并生成 response。Strapi 提供 `createCoreController` 自动生成默认 CRUD actions，同时允许新增、wrap 或完全替换 controller action。

**Original:** Controllers contain actions reached according to the requested route. As logic grows, use services for reusable pieces.

**中文译文:** Route 的 `handler` 会定位到 controller action。小型逻辑可以直接写在 controller 中，但随着复杂度增加，应把可复用业务逻辑下沉到 [services](/cms/backend-customization/services)。

**Original:** Always validate/sanitize overridden core actions to prevent leaking private fields or bypassing access rules.

**中文译文:** **Override core action 时必须重视 validation 与 sanitization。** 推荐使用：
- `validateQuery`：可选，遇到非法或无权限 query 时直接报错；
- `sanitizeQuery`：强烈推荐，移除不允许的 query parameters；
- `sanitizeOutput`：返回前清理 private / restricted fields。

## Implementation

**Original:** Controllers can be generated with `strapi generate` or created manually in `./src/api/[api-name]/controllers/`.

**中文译文:** API controller 可以通过 `strapi generate` 创建，也可以手动放在：
`./src/api/[api-name]/controllers/`。
Plugin controller 通常放在 plugin server 目录并通过 plugin interface export。

### Adding a new controller

**Original:** `createCoreController` can create a custom action, wrap a core action, or replace a core action.

**中文译文:** `createCoreController` 常见 3 种模式：
1. 新增自定义 action；
2. Wrap core action（调用 `super` 保留原逻辑）；
3. 完全替换 core action，并自行处理 query / output sanitization。

**Original code (kept unchanged):**

```js title="./src/api/restaurant/controllers/restaurant.js"
const { createCoreController } = require('@strapi/strapi').factories;

module.exports = createCoreController(
  'api::restaurant.restaurant',
  ({ strapi }) => ({
    async exampleAction(ctx) {
      try {
        ctx.body = 'ok';
      } catch (err) {
        ctx.body = err;
      }
    },

    async find(ctx) {
      ctx.query = { ...ctx.query, locale: 'en' };

      const { data, meta } = await super.find(ctx);

      meta.date = Date.now();

      return { data, meta };
    },

    async findCustom(ctx) {
      await this.validateQuery(ctx);

      const sanitizedQueryParams = await this.sanitizeQuery(ctx);
      const { results, pagination } =
        await strapi.service('api::restaurant.restaurant').find(
          sanitizedQueryParams
        );

      const sanitizedResults = await this.sanitizeOutput(results, ctx);

      return this.transformResponse(sanitizedResults, { pagination });
    },
  })
);
```

**中文译文:** 该示例分别展示：
- `exampleAction`：全新 custom action；
- `find`：在 `super.find(ctx)` 前后加入 custom logic；
- custom safe action：显式 validate / sanitize query，调用 service，sanitize output，并用 `transformResponse` 生成标准 REST response。

**Original:** Every controller action can be async or sync and receives Koa `ctx`.

**中文译文:** Controller action 可以是 sync / async function，都会接收 Koa `ctx`，其中包含 request、state 与 response context。

### Basic custom route/controller example

```js title="./src/api/hello/routes/hello.js"
module.exports = {
  routes: [
    {
      method: 'GET',
      path: '/hello',
      handler: 'api::hello.hello.index',
    }
  ]
}
```

```js title="./src/api/hello/controllers/hello.js"
module.exports = {
  async index(ctx, next) {
    ctx.body = 'Hello World!';
  },
};
```

**中文译文:** 请求 `GET /hello` 时，route handler 指向 `api::hello.hello.index`，因此 Strapi 执行 `hello.js` controller 的 `index` action。

## Controllers & Routes mapping

**Original:** Default content-type routes already map to `find`, `findOne`, `create`, `update`, and `delete`. Overriding these action names does not require route changes.

**中文译文:** Content-type 的 core routes 已经自动指向标准 CRUD action names。因此只要保留 action name 不变，override controller 实现后 router 会自动调用新逻辑，不需要重新定义 CRUD routes。

**Original:** New action names require a custom route whose handler points to the action.

**中文译文:** 如果增加全新 action（例如 `exampleAction`），则必须增加 custom route，让 HTTP request 能够到达该 action。

```js title="./src/api/restaurant/controllers/restaurant.js"
const { createCoreController } = require('@strapi/strapi').factories;

module.exports = createCoreController(
  'api::restaurant.restaurant',
  ({ strapi }) => ({
    async exampleAction(ctx) {
      const specials =
        await strapi.service('api::restaurant.restaurant').find({
          filters: { isSpecial: true },
        });

      return this.transformResponse(specials.results);
    },
  })
);
```

```js title="./src/api/restaurant/routes/01-custom-restaurant.js"
module.exports = {
  routes: [
    {
      method: 'GET',
      path: '/restaurants/specials',
      handler: 'api::restaurant.restaurant.exampleAction',
    },
  ],
};
```

**中文译文:** 这是推荐的“新增 action + custom route”组合方式，而无需复制所有已有 CRUD route definitions。

## Sanitization and Validation

**Original:** Sanitization cleans data; validation asserts that data is already valid and throws if not.

**中文译文:**
- **Sanitization**：清除 caller 不应访问或不合法的数据，并返回 cleaned object；
- **Validation**：断言输入本身是否合法；发现非法字段时直接抛出 error。

**Original:** Strapi 5 validates query params and create/update input data. Invalid relations, unknown schema fields, non-writable fields/internal timestamps, and setting an `id` can cause `400 Bad Request`.

**中文译文:** Strapi 5 对 query 与 create/update input 都执行 validation。以下情况可能返回 `400 Bad Request`：
- 创建 caller 无权限建立的 relation；
- Schema 中不存在的 unknown field；
- Non-writable fields 与 internal timestamps（如 `createdAt`、`createdBy`）；
- 尝试直接设置 / 更新 `id`（relation connect 的合法 identifier 用法除外）。

### Factory controller helpers

| Function | Parameters | 中文说明 |
|---|---|---|
| `sanitizeQuery` | `ctx` | 清理 request query |
| `sanitizeOutput` | entity/entities, `ctx` | 清理 response data |
| `sanitizeInput` | data, `ctx` | 清理 input data |
| `validateQuery` | `ctx` | 校验 request query |
| `validateInput` | data, `ctx` | Experimental：校验 input data |

**Original:** Helpers inherit schema/authentication sanitization rules automatically.

**中文译文:** 这些 factory helpers 会自动结合当前 controller 对应 content-type schema，以及 Content API authentication strategy（Users & Permissions / API token）执行权限敏感的 sanitization。

**Original:** If querying a different model from the current controller, do not use `this.sanitize*`; use `strapi.contentAPI` with the correct schema instead.

**中文译文:** **重要：** `this.sanitizeQuery()` / `this.sanitizeOutput()` 基于当前 controller 的 model。如果 restaurant controller 内实际查询的是另一个 model（例如 menu），不能用当前 model 的 sanitizer；应使用 `strapi.contentAPI.sanitize.*` 并显式传入正确 schema。

### Safe core-controller override

```js
async find(ctx) {
  await this.validateQuery(ctx);

  const sanitizedQueryParams = await this.sanitizeQuery(ctx);

  const { results, pagination } =
    await strapi.service('api::restaurant.restaurant').find(
      sanitizedQueryParams
    );

  const sanitizedResults = await this.sanitizeOutput(results, ctx);

  return this.transformResponse(sanitizedResults, { pagination });
}
```

**中文译文:** 这是 override core query action 的安全流程：
1. validate query；
2. sanitize query；
3. 调用 service；
4. sanitize output；
5. transform 成标准 REST response。

## Custom-controller sanitization with `strapi.contentAPI`

| Function | 中文说明 |
|---|---|
| `strapi.contentAPI.sanitize.input(data, schema, auth)` | 清理 request input、restricted relations、non-writable fields |
| `sanitize.output(data, schema, auth)` | 清理 private fields、passwords、restricted relations |
| `sanitize.query(query, schema, auth)` | 清理 filters / sort / fields / populate |
| `validate.query(query, schema, auth)` | 校验 query（当前 populate validation 仍有限制） |
| `validate.input(data, schema, auth)` | Experimental input validation |

**Original code (kept unchanged):**

```js
module.exports = {
  async findCustom(ctx) {
    const contentType = strapi.contentType('api::test.test');

    await strapi.contentAPI.validate.query(
      ctx.query,
      contentType,
      { auth: ctx.state.auth }
    );

    const sanitizedQueryParams =
      await strapi.contentAPI.sanitize.query(
        ctx.query,
        contentType,
        { auth: ctx.state.auth }
      );

    const documents =
      await strapi.documents(contentType.uid).findMany(
        sanitizedQueryParams
      );

    return await strapi.contentAPI.sanitize.output(
      documents,
      contentType,
      { auth: ctx.state.auth }
    );
  }
}
```

**中文译文:** 自定义 controller 查询任意 model 时，应显式获取 `contentType` schema，再传入 `ctx.state.auth`，确保 sanitization 与当前 caller permissions 一致。

## Extending core controllers

**Original:** Core actions can be wrapped with `super.find`, `super.findOne`, `super.create`, `super.update`, and `super.delete`.

**中文译文:** 如果只是给 core behavior 加前后处理，优先通过 `super.*` wrap：
- Collection type：`find`、`findOne`、`create`、`update`、`delete`；
- Single type：`find`、`update`、`delete`。

**Original:** Extending a core controller is preferred where possible because core sanitization remains in place.

**中文译文:** 能用 extend / wrap core controller 完成时，应优先这样做，因为 core controller 已内建相关 sanitization，减少手工遗漏安全处理的风险。

## Usage

**Original:** Controllers are normally invoked by routes and do not need to be called directly. They can be accessed programmatically with `strapi.controller()`.

**中文译文:** Controller 一般由 route 自动调用，无需手工 invoke。如果特殊场景需要 programmatic access：

```js
strapi.controller('api::api-name.controller-name');
strapi.controller('plugin::plugin-name.controller-name');
```

**Original:** Run `yarn strapi controllers:list` to list controllers.

**中文译文:** 可运行 `yarn strapi controllers:list` 查看当前已注册 controllers。
