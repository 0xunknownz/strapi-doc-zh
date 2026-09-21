# 📖 对照翻译：Backend customization

> Source: `docusaurus/docs/cms/backend-customization.md`  
> Upstream SHA: `11905d253699679defe4dd0a41a7ea4224318718`

**Original:** Strapi’s back end is a Koa-based server where requests pass through global middlewares, routes, controllers, services, and models before the Document Service returns responses.

**中文译文:** Strapi back end 是基于 Koa 的 HTTP server。Request 会依次经过 global middlewares、routes、policies / route middlewares、controllers、services 与 models，最终通过 Document Service / Query Engine 与 database 交互，再返回 response。

**Original:** In this documentation, "back end" specifically means the server part of Strapi, not Strapi as a whole.

**中文译文:** 在开发者文档中，**back end** 专指 Strapi 的 server 部分，而不是把整个 headless CMS 产品都泛称为 back end。

**Original:** Strapi has 2 parts: a back-end HTTP server and the admin panel front end.

**中文译文:** Strapi 自身包含两个主要部分：
- **Back end**：HTTP server，负责接收 request、返回 response，并与 database 交互执行内容 CRUD；
- **Admin panel**：Strapi 自带的 graphical UI，用于定义 content structure 与管理内容。

**Original:** The Strapi back end runs on Koa.

**中文译文:** Strapi back end 基于 [Koa](https://koajs.com/) 运行。

**Original:** REST and GraphQL APIs send requests to the back end to create, retrieve, update, or delete data.

**中文译文:** External application 可以通过 REST 或 GraphQL API 向 Strapi back end 发起 request，执行 create、retrieve、update、delete。

## Request flow

**Original:** A request can travel through the Strapi back end as follows:
1. Server receives request.
2. Global middlewares run sequentially.
3. Request matches a route.
4. Route policies validate access; route middlewares can mutate/control flow.
5. Controllers execute; services provide reusable custom logic.
6. Controllers/services interact with models through Document Service and Query Engine.
7. Document Service middlewares can intercept data before Query Engine; lifecycle hooks are lower-level alternatives.
8. Server returns response, which travels back through route/global middlewares.

**中文译文:** 一个 request 在 Strapi back end 中通常按以下路径流转：
1. Server 接收 [request](/cms/backend-customization/requests-responses)；
2. Request 依次经过 [global middlewares](/cms/backend-customization/middlewares)；
3. 根据 [route](/cms/backend-customization/routes) 匹配目标 handler；
4. [Policies](/cms/backend-customization/policies) 执行 read-only authorization / validation；route middlewares 可以修改 request 或控制执行流程；
5. [Controller](/cms/backend-customization/controllers) 执行 route action；[service](/cms/backend-customization/services) 可承载可复用业务逻辑；
6. Controller / service 根据 [models](/cms/backend-customization/models) 操作数据，推荐通过 Document Service API，必要时使用 Query Engine API；
7. 可以使用 [Document Service middlewares](/cms/api/document-service/middlewares) 在数据进入 Query Engine 前拦截；直接 database lifecycle hook 属于更低层机制；
8. Server 生成 response；response 再沿 route middlewares / global middlewares 的调用链返回。

**Original:** Global and route middlewares use an asynchronous `await next()` callback.

**中文译文:** Global middleware 与 route middleware 都遵循 Koa 风格的异步 `await next()` 调用链。

**Original:** If middleware calls `await next()`, processing continues through controllers/services/database layers. If it returns before calling `next()`, it can immediately send a response and skip downstream layers.

**中文译文:** Middleware 行为决定 request 是否继续：
- 调用 `await next()`：继续执行后续 middleware / controller / service / database 逻辑，然后 response 再回到当前 middleware；
- 在调用 `next()` 之前直接 return / 设置 response：可提前结束 request，跳过后续核心层。

**Original:** The customizations described in this section are for REST API. GraphQL has separate customization APIs.

**中文译文:** 本 Backend customization 章节主要描述 **REST API** request path 的 customization。GraphQL 的自定义机制请参阅 GraphQL plugin 文档。

## Interactive diagram

**Original:** The documentation includes an interactive diagram showing how requests travel through the back end.

**中文译文:** 官方页面提供 interactive diagram，可以按 request flow 点击 routes、middlewares、controllers、services、models 等节点跳转到对应文档。
