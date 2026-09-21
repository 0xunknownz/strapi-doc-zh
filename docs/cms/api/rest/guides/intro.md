# 📖 对照翻译：REST API Guides

> Source: `docusaurus/docs/cms/api/rest/guides/intro.md`  
> Upstream SHA: `080ad195b88afc5682d0c1a65830cbc1a789795b`

**Original:** Explore detailed guides and step-by-step instructions on specific REST API topics, including populate parameters and custom controllers for accessing creator fields.

**中文译文:** 本章节通过详细说明和分步指南深入介绍特定 REST API 主题，包括 `populate` parameter，以及通过 custom controller / middleware 返回 creator fields 的实现方式。

**Original:** The REST API reference documentation is meant to provide a quick reference for all endpoints and parameters available.

**中文译文:** [REST API reference](/cms/api/rest) 主要用于快速查阅全部 endpoints 与 parameters；本 Guides 章节则针对具体场景提供更完整的解释和操作步骤。

## Guides

**Original:** Official guides include detailed explanations (🧠) and step-by-step instructions (🛠️).

**中文译文:** Strapi Documentation 团队维护的 guides 分为：
- 🧠：概念与原理的深入解释；
- 🛠️：面向具体场景的分步操作说明。

**Original:** Understanding populate — Learn what populating means and how to use `populate` in REST API queries.

**中文译文:** **Understanding populate** —— 解释 population 的含义，以及如何在 REST API query 中使用 `populate` 添加额外 fields。参阅 [Understanding populate](/cms/api/rest/guides/understanding-populate)。

**Original:** How to populate creator fields — Build a custom controller/middleware to return `createdBy` and `updatedBy`.

**中文译文:** **How to populate creator fields** —— 通过自定义逻辑，让 API response 包含 `createdBy` 与 `updatedBy`。参阅 [creator fields guide](/cms/api/rest/guides/populate-creator-fields)。

## Additional resources

**Original:** Some additional resources were created for Strapi v4 and might not fully work with Strapi 5.

**中文译文:** 下方部分扩展教程最初面向 Strapi v4，可能无法直接适用于 Strapi 5。使用时应结合当前 API 行为进行验证。

**Original:** Additional blog topics include REST API basics, authentication, Fetch API usage, and using a CDN with REST API.

**中文译文:** 其他 Strapi Blog 教程涉及 REST API 基础、JWT / API token authentication、使用 Fetch API 请求 Content API，以及借助 CDN 降低大量 media asset 请求带来的网络延迟。
