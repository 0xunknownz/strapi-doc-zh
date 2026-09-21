# 📖 对照翻译：Routes

> Source: `docusaurus/docs/cms/backend-customization/routes.md`  
> Upstream SHA: `77e5ab938b5c5ab558e545b9ce842619c570700d`

**Original:** Routes map incoming URLs to controllers and ship pre-generated for each content type. This documentation shows how to add or customize core and custom routers and attach policies or middlewares for extra control.

**中文译文:** Route 负责把进入 Strapi 的 HTTP URL / method 映射到 controller action。Strapi 会为每个 content-type 自动生成 core routes，也允许开发者创建 custom router，并通过 policies、middlewares 与 authentication config 控制访问和 request flow。

**Original:** Requests sent to any Strapi URL are handled by routes. Routes can be configured with policies and middlewares.

**中文译文:** 所有进入 Strapi 的 HTTP request 都会先匹配 route。Route configuration 可以：
- 添加 [policy](/cms/backend-customization/policies) 阻止不符合条件的 request；
- 添加 [middleware](/cms/backend-customization/middlewares) 修改 request / response 或执行额外逻辑。

**Original:** Once a route exists, reaching it executes code handled by a controller. Run `yarn strapi routes:list` to list routes and their order.

**中文译文:** Route 匹配成功后，会执行其 `handler` 指向的 controller action。可以运行 `yarn strapi routes:list` 查看当前全部 routes 及加载顺序。

**Original:** If you only customize default controller actions (`find`, `findOne`, `create`, `update`, `delete`), you do not need to edit the router. Add/edit routes only for new paths/methods/actions.

**中文译文:** 如果只是 override content-type 默认 controller action（`find`、`findOne`、`create`、`update`、`delete`），**通常无需修改 router**。Core route 已经指向这些 action name。只有新增 HTTP path / method 或新增 controller action 时才需要 custom route。

## Implementation

**Original:** New routes live in `./src/api/[apiName]/routes`. There are 2 structures: core routers and custom routers.

**中文译文:** Route file 位于 `./src/api/[apiName]/routes`。主要有两种模式：
- 配置 Strapi 自动生成的 **core router**；
- 创建完全自定义的 **custom router**。

## Configuring core routers

**Original:** Core routers correspond to `find`, `findOne`, `create`, `update`, and `delete`, and are created automatically for content types.

**中文译文:** Core router 对应 REST API 默认 CRUD actions：`find`、`findOne`、`create`、`update`、`delete`。

**Original:** `createCoreRouter` accepts `prefix`, `only`, `except`, and `config`.

**中文译文:**

| Parameter | 中文说明 |
|---|---|
| `prefix` | 给该 model 的全部 core routes 增加自定义 path prefix |
| `only` | 只加载列出的 core routes |
| `except` | 排除列出的 core routes，与 `only` 作用相反 |
| `config` | 按 action 配置 `auth`、`policies`、`middlewares` 等 |

**Original code (kept unchanged):**

```js title="./src/api/restaurant/routes/restaurant.js"
const { createCoreRouter } = require('@strapi/strapi').factories;

module.exports = createCoreRouter('api::restaurant.restaurant', {
  prefix: '',
  only: ['find', 'findOne'],
  except: [],
  config: {
    find: {
      auth: false,
      policies: [],
      middlewares: [],
    },
    findOne: {},
    create: {},
    update: {},
    delete: {},
  },
});
```

**中文译文:** 上例只加载 `find` 与 `findOne`，并将 `find` 设置为 public route。未在 `only` 中列出的 core action 不会注册。

**Original:** A router with `only: ['find']` exposes only GET `/restaurants`. Fully-qualified handler names are recommended for custom actions.

**中文译文:** 例如只设置 `only: ['find']` 时，只保留 collection 的 GET list route。Custom action 建议使用 fully-qualified handler，如：
`api::restaurant.restaurant.review`。

## Creating custom routers

**Original:** A custom router exports an array of route objects with `method`, `path`, `handler`, and optional `config`.

**中文译文:** Custom router 由 route objects 组成：

| Parameter | 中文说明 |
|---|---|
| `method` | `GET` / `POST` / `PUT` / `DELETE` / `PATCH` |
| `path` | 以 `/` 开头的 URL path |
| `handler` | 要执行的 controller action |
| `config` | 可选 route config，包括 auth / policies / middlewares |

**Original:** Prefer fully-qualified API handlers: `api::<api-name>.<controllerName>.<actionName>`. Plugin handlers use `plugin::<plugin-name>.<controllerName>.<actionName>`.

**中文译文:** 推荐 handler 使用完整 UID：
- API controller：`api::<api-name>.<controllerName>.<actionName>`
- Plugin controller：`plugin::<plugin-name>.<controllerName>.<actionName>`

旧的 `<controllerName>.<actionName>` short form 仍兼容，但 fully-qualified form 更明确，也能避免不同 API / plugin 间 naming collision。

**Original:** Dynamic routes can use URL parameters and regular expressions. Parameters are exposed in `ctx.params`.

**中文译文:** Route path 支持 dynamic parameters 与 regular expression。匹配到的 URL parameter 可通过 `ctx.params` 读取。

**Original:** Route files load alphabetically. Prefix custom route filenames (e.g. `01-`) if they need to match before core routes.

**中文译文:** Route files 按 filename alphabetical order 加载。如果 custom route 可能被 core route 抢先匹配，可使用 `01-custom-routes.js`、`02-core-routes.js` 等命名控制顺序。

**Original code (kept unchanged):**

```js title="./src/api/restaurant/routes/01-custom-restaurant.js"
const config = {
  type: 'content-api',
  routes: [
    {
      method: 'POST',
      path: '/restaurants/:id/review',
      handler: 'api::restaurant.restaurant.review',
    },
    {
      method: 'GET',
      path: '/restaurants/:category([a-z]+)',
      handler: 'api::restaurant.restaurant.findByCategory',
    }
  ]
}

module.exports = config
```

**中文译文:** 第一条 route 使用 `:id` parameter；第二条通过 regular expression 限制 `:category` 只能由 lowercase letters 组成。

## Route configuration

**Original:** Core and custom routers use the same route config concepts.

**中文译文:** Core router 与 custom router 在 `config` 中共享同一套 access-control concepts。

### Policies

**Original:** Policies may be referenced by name, referenced with custom config, or declared inline.

**中文译文:** Route 中添加 policy 有 3 种方式：
- 引用已注册 policy name；
- 引用 policy，并传入自定义 config；
- 直接 inline 一个 policy function。

```js
policies: [
  'policy-name',
  { name: 'policy-name', config: {} },
  (policyContext, config, { strapi }) => {
    return true;
  },
]
```

**中文译文:** Policy 在 controller 前执行，适合 read-only authorization / validation。

### Middlewares

**Original:** Route middlewares can also be referenced by name, referenced with config, or declared inline.

**中文译文:** Route middleware 同样支持：
- middleware name；
- `{ name, config }`；
- inline `(ctx, next) => ...`。

```js
middlewares: [
  'middleware-name',
  { name: 'middleware-name', config: {} },
  (ctx, next) => {
    return next();
  },
]
```

**Original:** To run a middleware on all core actions, assign it under every core action, or build the config programmatically.

**中文译文:** `createCoreRouter` 的 middleware 是**按 action 配置**的。如果希望同一个 middleware 覆盖 `find`、`findOne`、`create`、`update`、`delete`，需要逐项配置，或通过 `Object.fromEntries()` 批量生成。

```js
const { createCoreRouter } = require('@strapi/strapi').factories;

const audit = ['global::audit-log'];
const actions = ['find', 'findOne', 'create', 'update', 'delete'];

module.exports = createCoreRouter('api::restaurant.restaurant', {
  config: Object.fromEntries(
    actions.map((action) => [action, { middlewares: audit }])
  ),
});
```

**中文译文:** 如果同时使用 `only` / `except`，`actions` array 应与实际注册的 routes 保持一致。

**Original:** Route-level middleware is recommended for centralized population rules to prevent over-fetching.

**中文译文:** Route middleware 很适合统一约束 `populate` rules，防止 accidental over-fetching，并保持 response size 可预测。

### Public routes

**Original:** Routes are protected by authentication by default. Set `auth: false` to make a route public/outside the normal Strapi authentication gate.

**中文译文:** Route 默认受 Strapi authentication system 保护（API tokens / Users & Permissions）。如果需要 public route，可设置：

```js
config: {
  auth: false
}
```

**中文译文:** `auth: false` 只表示跳过默认 authentication gate；仍然可以通过 policy / middleware 实现自定义访问控制。

## Custom Content API parameters

**Original:** Extra query/body parameters can be registered during the `register` lifecycle so they are validated and sanitized like built-in Content API parameters.

**中文译文:** Strapi 5 允许在 `register` lifecycle 中注册额外 Content API query / body parameters。注册后，这些 parameters 会像 core parameters 一样进入 validation / sanitization 流程，无需为每个额外 parameter 单独创建 custom route/controller。

**Original:** Enable strict parameters with `rest.strictParams: true`.

**中文译文:** 若希望未知 query/body keys 直接被拒绝，可在 `./config/api.js|ts` 中启用：

`rest.strictParams: true`

**Original:** Use `strapi.contentAPI.addQueryParams()` for extra query parameters and `addInputParams()` for root-level body keys.

**中文译文:**
- `strapi.contentAPI.addQueryParams()`：注册额外 query keys；
- `strapi.contentAPI.addInputParams()`：注册 root-level body keys，例如与 `data` 并列的 `clientMutationId`。

**Original:** Query schemas must be scalar or arrays of scalars. Input schemas can use any Zod type.

**中文译文:** Query parameter schema 必须是 scalar 或 scalar array（string / number / boolean / enum）；复杂 nested structure 应使用 `addInputParams`。Schema 使用 `@strapi/utils` 提供的 `z`（或 `zod/v4`）。

**Original:** `matchRoute` can restrict a parameter to selected routes.

**中文译文:** 每个注册项都可提供 `matchRoute(route)` callback，根据 `route.method`、`route.path`、`route.handler`、`route.info` 控制该 parameter 只在特定 routes 上启用。

**Original code (kept unchanged):**

```js title="./src/index.js"
module.exports = {
  register({ strapi }) {
    strapi.contentAPI.addQueryParams({
      search: {
        schema: (z) => z.string().max(200).optional(),
        matchRoute: (route) => route.path.includes('articles'),
      },
    });

    strapi.contentAPI.addInputParams({
      clientMutationId: {
        schema: (z) => z.string().max(100).optional(),
      },
    });
  },
};
```

**中文译文:** 上例只为 path 中包含 `articles` 的 routes 注册 `?search=`，并为 request body 全局允许可选 `clientMutationId`。

**Original:** Core query parameter names such as `filters`, `sort`, and `fields`, and reserved body names such as `id`/`documentId`, cannot be re-registered.

**中文译文:** 已有 core query names（如 `filters`、`sort`、`fields`）以及保留 input names（如 `id`、`documentId`）不能覆盖注册。
