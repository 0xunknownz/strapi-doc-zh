# 📖 对照翻译：Query Engine API

> Source: `docusaurus/docs/cms/api/query-engine.md`  
> Upstream SHA: `74c72a40905add3cc1ced79c8439583f68a8b9d9`

**Original:** The Query Engine API provides low-level, unrestricted backend access to Strapi's database layer through `strapi.db.query`, supporting single and bulk operations with filtering, populating, ordering, and pagination.

**中文译文:** Query Engine API 通过 `strapi.db.query` 提供低层、限制较少的 back-end database access，支持 single / bulk operations、filtering、populate、ordering 和 pagination。

**Original:** The Strapi backend provides a Query Engine API to interact with the database layer at a lower level.

**中文译文:** Query Engine API 位于 Document Service API 之下，更接近 database layer。

**Original:** In most cases, use Document Service API instead. Query Engine should only be used when you intentionally need row-level low-level access.

**中文译文:** **绝大多数场景不要直接使用 Query Engine API，而应优先使用 Document Service API。** 只有明确需要直接操作 database row、并理解相关风险时，才考虑 Query Engine。

**Original:** Query Engine is not aware of advanced Strapi 5 features such as Draft & Publish, Internationalization, Content History, and it uses `id` rather than `documentId`.

**中文译文:** Query Engine API 不理解 Draft & Publish、Internationalization、Content History 等 Strapi 5 高级语义，也不使用 `documentId`，而是基于 database `id`。错误使用可能导致数据库层面的非预期结果或与 Strapi 5 功能不完整兼容。

**Original:** Before using Query Engine, read the backend customization and Content API introductions.

**中文译文:** 深入使用 Query Engine 前，建议先阅读 [backend customization introduction](/cms/backend-customization) 与 [Content API introduction](/cms/api/content-api)。

## Basic usage

**Original:**
```js
strapi.db.query('api::blog.article').findMany({
  where: {
    title: {
      $startsWith: '2021',
      $endsWith: 'v4',
    },
  },
  populate: {
    category: true,
  },
});
```

**中文译文:** Query Engine 通过 `strapi.db.query('uid')` 使用。上例查询 title 以 `2021` 开头且以 `v4` 结尾的 article rows，同时 populate `category` relation。

## Available operations

**Original:** Query Engine supports single operations, bulk operations, filters, populate, and order & pagination.

**中文译文:** Query Engine API 主要能力包括：
- [Single operations](/cms/api/query-engine/single-operations)：单条 database entry 的 CRUD；
- [Bulk operations](/cms/api/query-engine/bulk-operations)：批量操作；
- [Filters](/cms/api/query-engine/filtering)：筛选；
- [Populate](/cms/api/query-engine/populating)：relations population；
- [Order & Pagination](/cms/api/query-engine/order-pagination)：排序和分页。
