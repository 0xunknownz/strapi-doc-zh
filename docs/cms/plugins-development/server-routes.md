# 📖 对照翻译：Server API — Routes

> Source: `docusaurus/docs/cms/plugins-development/server-routes.md`  
> Upstream SHA: `3f571272a0743ff185178b196033e72c22206806`

**Original:** The Server API exports a `routes` value to expose plugin endpoints. Use array, named-router, or factory-callback formats depending on the use case.

**中文译文:** Plugin Server API 通过 `routes` 暴露 HTTP endpoints，并把 incoming request 映射到 controller action。根据复杂度可使用 3 种 declaration format：
- Array format：简单 admin routes；
- Named router format：显式区分 Admin / Content API，推荐大多数 plugin 使用；
- Factory callback format：route config 需要读取 runtime plugin config 等高级场景。

## Array format

**Original:** An array of route objects is registered as admin routes by default and gets the plugin-name prefix automatically.

**中文译文:** 直接 export route array 时，Strapi 默认把它当作 **Admin route** 注册，并自动加 plugin prefix。

```js
module.exports = [
  {
    method: 'GET',
    path: '/articles',
    handler: 'article.find',
    config: {
      policies: [],
    },
  },
  {
    method: 'POST',
    path: '/articles',
    handler: 'article.create',
    config: {
      policies: [],
    },
  },
];
```

**中文译文:** 若需要 Content API route，不要依赖 array format，应使用 named router 并显式设置 `type: 'content-api'`。

## Named router format

**Original:** Named groups can separate `admin` and `content-api` routers.

**中文译文:** Named router 用 object key 组织多个 router group，每个 group 可指定 `type`、`prefix`、`routes`。

```js
module.exports = {
  admin: {
    type: 'admin',
    routes: [
      {
        method: 'GET',
        path: '/articles',
        handler: 'article.find',
        config: {
          policies: ['admin::isAuthenticatedAdmin'],
        },
      },
    ],
  },

  'content-api': {
    type: 'content-api',
    routes: [
      {
        method: 'GET',
        path: '/articles',
        handler: 'article.find',
        config: {
          policies: [],
        },
      },
    ],
  },
};
```

**中文译文:** 这种形式清楚表达哪些 endpoint 面向 admin panel、哪些属于 Content API，因此最适合同时提供两类 API 的 plugin。

## Factory callback format

**Original:** Use a factory when route configuration depends on the `strapi` instance.

**中文译文:** 如果 route 是否 public、path、policy 等需要根据 plugin configuration 动态决定，可以给 named route entry 提供 factory callback。

```js
module.exports = {
  'content-api': ({ strapi }) => ({
    type: 'content-api',
    routes: [
      {
        method: 'GET',
        path: '/articles',
        handler: 'article.find',
        config: {
          auth:
            strapi
              .plugin('my-plugin')
              .config('publicRead')
              ? false
              : {},
        },
      },
    ],
  }),
};
```

**Original:** A factory callback is only valid under a named route entry, not as the root export.

**中文译文:** 注意 factory callback 必须挂在 `admin`、`content-api` 等 named entry 下。Root-level `module.exports = ({ strapi }) => ...` **不是有效 routes format**。

## Defaults applied by Strapi

| Property | Default | 中文说明 |
|---|---|---|
| `type` | `admin` | Array format 或未指定 type 时默认 admin |
| `prefix` | `/<plugin-name>` | 自动使用 plugin name 作为 URL prefix |
| `config.auth.scope` | `plugin::<plugin-name>.<handler>` | 对 string handler 自动生成 permission scope |

**Original:** Existing auth values are preserved using deep-default behavior.

**中文译文:** 自动生成 auth scope 使用 defaults merge，不会覆盖 developer 已明确提供的配置。

## Route config — policies

**Original:** Policies can be strings, inline functions, or `{ name, options }` objects.

**中文译文:** `config.policies` 支持：
- Namespaced policy string；
- Inline policy function；
- `{ name, options }`，将 `options` 传入 policy 的 config argument。

```js
policies: [
  'plugin::my-plugin.isActive',
  {
    name: 'plugin::my-plugin.hasRole',
    options: {
      role: 'editor',
    },
  },
]
```

## Route config — middlewares

**Original:** Route middleware entries use strings, inline handlers, or `{ name, options }`.

**中文译文:** `config.middlewares` 同样支持 namespaced string、inline middleware 与 `{ name, options }`。

**Original:** Internal support for `{ resolve, config }` exists, but standard route validation rejects it.

**中文译文:** 某些 Strapi internals 仍保留 `{ resolve, config }` middleware shape，但标准 plugin route validation 会拒绝这种形式。**应使用 `{ name, options }`**。

## Route config — auth

**Original:** `auth` can be `false` or an object containing `scope` and optional `strategies`.

**中文译文:**
- `auth: false`：跳过默认 authentication，route 变为 public；
- `auth: { scope, strategies? }`：定义 permission scope，并可选择 authentication strategies。

**Original:** String handlers get automatic auth-scope generation; inline function handlers do not.

**中文译文:** 使用 `handler: 'article.find'` 这类 string handler 时，Strapi 会自动补默认 `auth.scope`。Inline function handler **不会自动得到 scope**，需要显式配置。

**Original:** Disabling auth on an admin route is almost never intentional.

**中文译文:** 对 Admin route 设置 `auth: false` 等于允许 unauthenticated request 访问 admin endpoint，通常属于严重安全风险，应谨慎使用。

## Best practices

**中文译文:**
- 同时提供 Admin / Content API 时优先 named router；
- Handler 尽量使用 string，让 Strapi 能自动生成 auth scope；
- Plugin policy 使用完整 `plugin::my-plugin.policy-name` namespace；
- Admin route 不要轻易关闭 auth；
- Route 数量增长后按 resource 拆文件，再从 index re-export。
