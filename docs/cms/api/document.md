# 📖 对照翻译：Documents

> Source: `docusaurus/docs/cms/api/document.md`  
> Upstream SHA: `4e27f0f97bd3bb0996942245404e70b4df47acd9`

**Original:** A document is an API-only concept representing all content variations (locales, draft/published versions) for a single content-type entry. Use the Document Service API to manipulate documents on the back-end.

**中文译文:** Document 是 Strapi 5 中一个只在 API 层出现的概念，用来表示某个 content-type entry 的所有内容变体，包括不同 locales 以及 draft / published versions。Back-end 中使用 Document Service API 操作 documents。

**Original:** A document represents all different variations of content for a given entry.

**中文译文:** 一个 document 相当于某个逻辑 entry 的“容器”，把该 entry 的所有版本统一组织在一起。

**Original:** A single type contains one unique document, while a collection type can contain several documents.

**中文译文:** Single type 只包含一个唯一 document；collection type 则可以包含多个 documents。

**Original:** The admin panel does not expose the document concept. Users create and edit entries in Content Manager.

**中文译文:** Admin panel 中不会直接向最终用户展示 “document” 这一概念。用户在 Content Manager 里看到和编辑的是 **entries**。

**Original:** At API level, an entry's fields can differ by locale and by draft/published version.

**中文译文:** 但在 API 层，同一个逻辑 entry 的 field value 可能：
- 在 English / French 等不同 locales 中不同；
- 在同一 locale 的 draft 与 published version 中也不同。

**Original:** The bucket that contains all draft and published versions for all locales is a document.

**中文译文:** 把所有 locales 的 draft / published versions 聚合在一起的逻辑容器，就是 document。

**Original:** Document Service API can create, retrieve, update, and delete entire documents or specific subsets of their data.

**中文译文:** Document Service API 可以创建、读取、更新、删除完整 document，也可以只操作其中某个 locale 或某个 status version。

**Original:** If i18n is enabled, a document can have multiple document locales. If Draft & Publish is enabled, each locale can have a draft and published version.

**中文译文:** 如果 content-type 启用了 Internationalization，一个 document 可以有多个 document locales；如果启用了 Draft & Publish，则对应 locale 还可以同时拥有 draft 与 published versions。

**Original:** From backend controllers, services, or plugins use Document Service API. From frontend use REST or GraphQL.

**中文译文:** API 选择建议：
- Back-end controller、service、plugin：使用 [Document Service API](/cms/api/document-service)；
- Front-end application：使用 [REST API](/cms/api/rest) 或 [GraphQL API](/cms/api/graphql)。

**Original:** Document Service returns draft by default; REST and GraphQL return published by default.

**中文译文:** 一个重要差异是默认版本：
- Document Service API 默认返回 **draft**；
- REST API 与 GraphQL API 默认返回 **published**。
