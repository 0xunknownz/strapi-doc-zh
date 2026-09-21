# 📖 对照翻译：Strapi APIs to access your content

> Source: `docusaurus/docs/cms/api/content-api.md`  
> Upstream SHA: `ba466e91886f951e1c01884d94daff9e7404df60`

**Original:** Strapi's Content API provides access to your content through REST and GraphQL APIs for front-end applications, plus lower-level Document Service and Query Engine APIs for backend and plugin development.

**中文译文:** Strapi 的 Content API 为 front-end application 提供 REST 与 GraphQL 两种外部访问方式，同时也提供更底层的 Document Service API 与 Query Engine API，供 back-end customization 和 plugin development 使用。

**Original:** Once you have created a project, built a content structure, and added data, you will likely want to access your content.

**中文译文:** 创建 Strapi 项目、通过 Content-Type Builder 定义 content structure，并在 Content Manager 添加数据后，下一步通常就是通过 API 访问这些内容。

**Original:** From a front-end application, content is exposed by default through REST API and optionally through GraphQL API if the GraphQL plugin is installed.

**中文译文:** 从 front-end application 访问内容时：
- REST API 默认可用；
- 安装 Strapi 内置 GraphQL plugin 后，也可以使用 GraphQL API。

**Original:** You can also use the Strapi Client library to interact with REST API.

**中文译文:** 也可以使用 [Strapi Client](/cms/api/client) library 与 REST API 交互。

**Original:** REST and GraphQL are top-level Content API layers exposed to external applications. Strapi also provides 2 lower-level APIs.

**中文译文:** REST 与 GraphQL 属于面向外部 application 的 Content API 顶层接口；Strapi 还提供 2 个 lower-level back-end APIs。

**Original:** The Document Service API, available through `strapi.documents`, is the recommended API for interacting with the database from the backend server or plugins. It understands documents, components, and dynamic zones.

**中文译文:** [Document Service API](/cms/api/document-service) 通过 `strapi.documents` 使用，是在 back-end server 或 plugin 中操作应用数据的**推荐方式**。它理解 Strapi 的 document model，以及 components、dynamic zones 等复杂内容结构。

**Original:** The Query Engine API, available through `strapi.db.query`, is a lower-level unrestricted database layer. It is not aware of Draft & Publish, Internationalization, Content History, and other advanced Strapi features. In most cases you should use Document Service instead.

**中文译文:** [Query Engine API](/cms/api/query-engine) 通过 `strapi.db.query` 使用，提供更低层、限制更少的 database access。但它不了解 Draft & Publish、Internationalization、Content History 等高级 Strapi 5 语义。绝大多数场景应优先使用 Document Service API。

**Original:** The API documentation includes REST API, GraphQL API, Strapi Client, Document Service API, and OpenAPI Specification.

**中文译文:** 本章节主要包含：
- [REST API](/cms/api/rest)；
- [GraphQL API](/cms/api/graphql)；
- [Strapi Client](/cms/api/client)；
- [Document Service API](/cms/api/document-service)；
- [OpenAPI Specification](/cms/api/openapi)。

**Original:** For integrations with Next.js, Astro, Angular, and other platforms, see the Strapi integrations pages.

**中文译文:** 如果需要了解 Strapi 与 Next.js、Astro、Angular 等平台的集成方式，请参阅 Strapi 官方 integrations 页面。
