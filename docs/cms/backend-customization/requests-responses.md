# 📖 对照翻译：Requests and Responses

> Source: `docusaurus/docs/cms/backend-customization/requests-responses.md`  
> Upstream SHA: `1074039522d5f590a8aa6037e47c90371cea5920`

**Original:** Koa’s context (`ctx`) carries request info, state, and response data through every Strapi endpoint. This documentation details `ctx.request`, `ctx.state`, and `ctx.response`, plus a helper for accessing context anywhere.

**中文译文:** Strapi 基于 Koa，`ctx` context object 会贯穿一次 HTTP request 的后端执行链。本页介绍 `ctx.request`、`ctx.state`、`ctx.response`，以及如何通过 `strapi.requestContext` 在调用链深处读取当前 context。

**Original:** A context object is passed to policies, controllers, services, and other backend elements when REST requests are handled.

**中文译文:** REST API request 进入 Strapi 后，Koa context 会传递给 policies、controllers、middlewares 等后端元素；service 也可通过 request context helper 获取它。

**Original:** `ctx` includes:
- `ctx.request` for client request information
- `ctx.state` for backend request state
- `ctx.response` for outgoing response information

**中文译文:** `ctx` 的 3 个核心区域：
- `ctx.request`：客户端发来的 request 信息；
- `ctx.state`：当前 request 在 Strapi back end 中的状态；
- `ctx.response`：server 准备返回的 response。

## `ctx.request`

| Parameter | 中文说明 | Type |
|---|---|---|
| `ctx.request.body` | 已 parse 的 request body | Object |
| `ctx.request.files` | Request 携带的 files | Array |
| `ctx.request.headers` | Request headers | Object |
| `ctx.request.host` | URL host，包含 port | String |
| `ctx.request.hostname` | URL host，不包含 port | String |
| `ctx.request.href` | 完整 request URL（protocol/domain/port/path/query） | String |
| `ctx.request.ip` | Client IP | String |
| `ctx.request.ips` | 启用 proxy 且存在 `X-Forwarded-For` 时的 IP chain | Array |
| `ctx.request.method` | HTTP method，例如 GET / POST | String |
| `ctx.request.origin` | Protocol + host | String |
| `ctx.request.params` | Route path params，例如 `:id` | Object |
| `ctx.request.path` | 不含 query 的 path | String |
| `ctx.request.protocol` | `http` / `https` | String |
| `ctx.request.query` | Strapi REST query parameters | Object |
| `ctx.request.subdomains` | URL subdomains | Array |
| `ctx.request.url` | Path + query，不含 protocol/domain/port | String |

### URL property comparison

**Original:** For `https://example.com:1337/api/restaurants?id=123`:
- `href` is full URL
- `protocol` is `https`
- `origin` is `https://example.com:1337`
- `url` is `/api/restaurants?id=123`
- `path` is `/api/restaurants`

**中文译文:** 这些属性用于不同粒度地访问 URL。需要注意 `host` 包含 port，而 `hostname` 不包含；`href` 是完整 URL，`url` 则仅包含 path + query。

### `ctx.request.query`

| Parameter | 中文说明 |
|---|---|
| `ctx.request.query` / `ctx.query` | 完整 query object |
| `sort` | REST sorting |
| `filters` | REST filters |
| `populate` | Relations/components/dynamic zones population |
| `fields` | Field selection |
| `pagination` | Pagination |
| `publicationState` | Draft & Publish state（旧命名/兼容 context） |
| `locale` | Locale selection |

**中文译文:** 这些 query values 对应 REST API parameters。处理 custom controller 时，应继续注意 sanitization / validation，而不是直接信任 client query。

## `ctx.state`

**Original:** `ctx.state` stores request state such as authentication and route data.

**中文译文:** `ctx.state` 存放当前 request 在 Strapi back end 中经过 authentication / routing 后形成的 state。

| Parameter | 中文说明 |
|---|---|
| `ctx.state.isAuthenticated` | 当前 request 是否通过任意 authentication strategy |

### `ctx.state.user`

| Parameter | 中文说明 |
|---|---|
| `ctx.state.user` | 当前 user 信息 |
| `ctx.state.user.role` | User role |

**中文译文:** 对通过 Users & Permissions authentication 的 Content API request，常用 `ctx.state.user` 获取当前 end-user identity。

### `ctx.state.auth`

| Parameter | 中文说明 |
|---|---|
| `ctx.state.auth.strategy` | 当前 authentication strategy 信息 |
| `ctx.state.auth.strategy.name` | Strategy name |
| `ctx.state.auth.credentials` | 当前 credentials |

**中文译文:** `ctx.state.auth` 描述 request 当前使用的 authentication strategy，例如 Users & Permissions 或 API token。

### `ctx.state.route`

| Parameter | 中文说明 |
|---|---|
| `ctx.state.route.method` | 当前 route HTTP method |
| `ctx.state.route.path` | Route path |
| `ctx.state.route.config` | Route config |
| `ctx.state.route.handler` | Controller handler |
| `ctx.state.route.info` | Route metadata |
| `ctx.state.route.info.apiName` | API name |
| `ctx.state.route.info.type` | API request type |

## `ctx.response`

| Parameter | 中文说明 | Type |
|---|---|---|
| `ctx.response.body` | Response body | Any |
| `ctx.response.status` | HTTP status code | Integer |
| `ctx.response.message` | Status message | String |
| `ctx.response.header(s)` | Response headers | Object |
| `ctx.response.length` | `Content-Length` 或可推导 body length | Integer |
| `ctx.response.redirect(url, [alt])` | 发送 302 redirect | Function |
| `ctx.response.attachment([filename], [options])` | 设置 `Content-Disposition: attachment` | Function |
| `ctx.response.type` | `Content-Type`，不含 charset 等 params | String |
| `ctx.response.lastModified` | `Last-Modified` header | DateTime |
| `ctx.response.etag` | 设置 response `ETag` | String |

**Original:** `ctx.response.redirect('back', '/index.html')` redirects to the Referrer or fallback URL.

**中文译文:** `redirect('back', fallback)` 会优先回到 Referrer；没有 Referrer 时使用 fallback（或默认 `/`）。

## Accessing request context anywhere

**Original:** Strapi exposes `strapi.requestContext.get()` to access the current HTTP request context from deeper code, such as services or lifecycle functions.

**中文译文:** Strapi 提供 `strapi.requestContext.get()`，可以在 service、lifecycle 等没有直接接收 `ctx` parameter 的深层代码中读取当前 HTTP request context。

```js
const ctx = strapi.requestContext.get();
```

**Original:** Only call this inside functions that are running as part of an HTTP request.

**中文译文:** 只能在**当前确实处于 HTTP request async context 内**的 function 中调用。不要在 module 顶层提前读取并缓存 `ctx`。

**Original — Correct:**
```js
const service = {
  myFunction() {
    const ctx = strapi.requestContext.get();
    console.log(ctx.state.user);
  },
};
```

**中文译文:** 正确做法是在 function 执行时获取 context。

**Original — Incorrect:**
```js
const ctx = strapi.requestContext.get();

const service = {
  myFunction() {
    console.log(ctx.state.user);
  },
};
```

**中文译文:** 错误做法是在 module 初始化阶段获取 context；此时通常没有有效 HTTP request。

### Lifecycle example

```js
module.exports = {
  beforeUpdate() {
    const ctx = strapi.requestContext.get();

    console.log('User info in service: ', ctx.state.user);
  },
};
```

**中文译文:** 如果 lifecycle 是由 HTTP request 触发，上例可以读取发起操作的 user 信息。

**Original:** Strapi uses Node.js `AsyncLocalStorage` to make context available across the async call chain.

**中文译文:** 该能力底层基于 Node.js `AsyncLocalStorage`，因此 context 可以沿当前 asynchronous execution chain 传播。

**Original:** For authenticated HTTP requests from admin-panel plugins, use Admin Panel API Fetch client.

**中文译文:** 如果是在 admin panel plugin 中发起 authenticated HTTP request，请使用 [Admin Panel API Fetch client](/cms/plugins-development/admin-fetch-client)。
