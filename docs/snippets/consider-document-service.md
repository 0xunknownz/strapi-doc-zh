# 📖 对照翻译：Prefer Document Service over Query Engine

> Source: `docusaurus/docs/snippets/consider-document-service.md`  
> Upstream SHA: `1118db6aa0755a5cf04da4a732723cece5a3b193`

**Original:** In most cases you should not use the Query Engine API and should use the Document Service API instead.

**中文译文:** 在绝大多数场景中，不应直接使用 Query Engine API，而应优先使用 [Document Service API](/cms/api/document-service)。

**Original:** Only use Query Engine if you know exactly what you are doing, for instance when you intentionally need a lower-level API that directly interacts with unique database rows.

**中文译文:** 只有在你明确理解其行为，并且确实需要直接操作 database unique rows 等低层能力时，才使用 Query Engine API。

**Original:** Query Engine is not aware of advanced Strapi 5 features such as Draft & Publish, Internationalization, Content History, and possibly more.

**中文译文:** Query Engine API 不理解 Draft & Publish、Internationalization、Content History 等 Strapi 5 高级功能的业务语义。

**Original:** Query Engine cannot use `documentId` and uses `id`, which can lead to unintended database consequences or partial compatibility with Strapi 5 features.

**中文译文:** Query Engine 使用 database `id` 而不是 `documentId`。因此，不恰当使用可能造成 database-level 的非预期结果，或者只与 Strapi 5 高级功能部分兼容。
