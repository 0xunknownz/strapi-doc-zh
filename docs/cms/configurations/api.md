# 📖 对照翻译：API configuration

> Source: `docusaurus/docs/cms/configurations/api.md`  
> Upstream SHA: `5d22b13e098d9305ffac8214a4f72e7e9cf7426e`

**Original:** `/config/api` centralizes response privacy, REST defaults, and strict parameter validation for both the REST Content API and the Document Service.

**中文译文:** `./config/api.js|ts` 集中配置 Content API response privacy、REST defaults，以及 REST Content API 与 Document Service 的 strict parameter validation。

| Property | Type | Default | 中文说明 |
|---|---|---:|---|
| `responses.privateAttributes` | String[] | `[]` | 全局视为 private 的 attributes |
| `rest.prefix` | String | `/api` | REST API prefix |
| `rest.defaultLimit` | Integer | `25` | Offset pagination 默认 `limit` |
| `rest.maxLimit` | Integer | `100` | REST request 允许的最大 `limit` |
| `rest.withCount` | Boolean | `true` | Collection response 默认是否执行 count 并返回 total / pageCount |
| `rest.strictParams` | Boolean | — | 是否拒绝未知 REST query/body root keys |
| `documents.strictParams` | Boolean | — | 是否拒绝 `strapi.documents()` 中未知 root-level parameters |

**Original:** If `rest.maxLimit` is less than `rest.defaultLimit`, `maxLimit` wins.

**中文译文:** 如果 `rest.maxLimit < rest.defaultLimit`，实际使用的 limit 会受 `maxLimit` 限制。

## Strict parameters

**Original:** `rest.strictParams` applies to incoming REST Content API requests. Extra parameters can be registered through `contentAPI.addQueryParams` / `addInputParams`.

**中文译文:** `rest.strictParams: true` 会让 REST Content API 只接受：
- Core parameters；
- Route schema 中声明的 parameters；
- 通过 `strapi.contentAPI.addQueryParams()` / `addInputParams()` 注册的自定义 parameters。

未知 top-level query/body key 会被拒绝。

**Original:** `documents.strictParams` applies to server-side `strapi.documents()` calls and rejects unrecognized root-level keys.

**中文译文:** `documents.strictParams: true` 则作用于 server-side Document Service。传入未知 root-level key（例如错误拼写的 `status` / `locale`）时会报错；未启用时通常会忽略未知 key。

**Original:** Projects scaffolded with `create-strapi-app` enable both strict options by default.

**中文译文:** 当前通过 `create-strapi-app` 创建的项目，其生成的 `config/api.*` 默认会把 `rest.strictParams` 和 `documents.strictParams` 都设为 `true`。

## Example

**Original code (kept unchanged):**

```js title="./config/api.js"
module.exports = ({ env }) => ({
  responses: {
    privateAttributes: ['_v', 'id', 'created_at'],
  },
  rest: {
    prefix: '/v1',
    defaultLimit: 100,
    maxLimit: 250,
    strictParams: true,
  },
  documents: {
    strictParams: true,
  },
});
```

**中文译文:** 该示例：
- 将指定 attributes 全局设为 private；
- 把 REST prefix 改为 `/v1`；
- 调整 default / max pagination limits；
- 同时启用 REST 与 Document Service strict parameter validation。
