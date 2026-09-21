# 📖 对照翻译：Entity Service API

> Source: `docusaurus/docs/cms/api/entity-service.md`  
> Upstream SHA: `573337bf86512002f158cd2f2365cb7c4227575f`

**Original:** The Entity Service API is a backend layer that handles complex content structures like components and dynamic zones, providing CRUD operations, filtering, populating relations, and pagination via `strapi.entityService`.

**中文译文:** Entity Service API 是 Strapi v4 时代的 back-end data layer，通过 `strapi.entityService` 支持 CRUD、filtering、populate relation 与 pagination，并能够处理 components、dynamic zones 等复杂内容结构。

**Original:** The Entity Service API is deprecated in Strapi v5. Use Document Service API instead.

**中文译文:** **Entity Service API 在 Strapi 5 中已经 deprecated。新代码应使用 Document Service API。**

**Original:** Before diving deeper, read the backend customization and Content API introductions.

**中文译文:** 如果正在维护旧项目并需要理解 Entity Service，建议先阅读 [backend customization](/cms/backend-customization) 与 [Content API](/cms/api/content-api) introductions。

**Original:** Entity Service is built on top of Query Engine API and handles Strapi complex content structures while Query Engine executes lower-level database queries.

**中文译文:** Entity Service 构建在 Query Engine API 之上：Query Engine 负责执行较低层 database queries，Entity Service 则增加对 components、dynamic zones 等 Strapi 内容结构的理解。

**Original:** Document Service is now the recommended layer; Query Engine should be used only if the higher-level API does not cover the use case; direct Knex access is available through `strapi.db.connection`.

**中文译文:** Strapi 5 当前推荐的层级为：
1. 优先使用 Document Service API；
2. Document Service 无法覆盖且确实需要低层访问时，才使用 Query Engine API；
3. 如果必须直接调用 Knex，可通过 `strapi.db.connection`。

**Original:** Services and Entity Service API are not directly related, even though services may call Entity Service.

**中文译文:** 注意不要把 [services](/cms/backend-customization/services) 与 Entity Service API 混淆。Service 可以调用 Entity Service，但二者是不同概念。

## Basic usage

**Original:**
```js
const entry = await strapi.entityService.findOne('api::article.article', 1, {
  populate: { someRelation: true },
});
```

**中文译文:** 旧 Entity Service 通过 `strapi.entityService` 调用，并使用 numeric `id`。在 Strapi 5 新代码中应迁移到 Document Service 的 `documentId` model。

## Available operations

**Original:** Entity Service historically supports CRUD, Filters, Populate, Order & Pagination, and Components/Dynamic Zones operations.

**中文译文:** 旧 Entity Service 文档包含 CRUD、Filters、Populate、Order & Pagination、Components / Dynamic Zones 等操作。它们主要用于维护和迁移 Strapi v4 代码，不建议作为 Strapi 5 新项目的首选 API。
