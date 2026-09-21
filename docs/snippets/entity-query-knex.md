# 📖 对照翻译：Backend data-access layers

> Source: `docusaurus/docs/snippets/entity-query-knex.md`  
> Upstream SHA: `8d713227f9080bb868ae98c964b08e34de0a17f8`

**Original:** Strapi offers several layers to interact with the backend and build queries.

**中文译文:** Strapi 提供多个 back-end data-access layers，可以根据抽象层级和使用场景选择。

**Original:** The Document Service API is the recommended API to interact with the application's database. It understands the document model, components, and dynamic zones.

**中文译文:** **Document Service API 是推荐方式。** 它理解 Strapi 的 document model，以及 components、dynamic zones 等复杂内容结构。

**Original:** The Query Engine API interacts with the database at a lower level and should only be used when Document Service does not cover the use case.

**中文译文:** Query Engine API 更接近 database layer，只应在 Document Service 无法覆盖具体场景、且你明确理解低层数据库语义时使用。

**Original:** If you need direct access to Knex functions, use `strapi.db.connection`.

**中文译文:** 如果确实需要直接调用 Knex functions，可使用 `strapi.db.connection`。
