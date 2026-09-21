# 📖 对照翻译：IDs in Strapi 5 responses

> Source: `docusaurus/docs/snippets/id-in-responses.md`  
> Upstream SHA: `e70f0e6e4707edf285aebd8fc3d744d3f0211c84`

**Original:** Though it's recommended to target entries by their `documentId` in Strapi 5, entries might still have an `id` field, and you will see it in the returned response. This should ease your transition from Strapi 4.

**中文译文:** Strapi 5 建议使用 `documentId` 定位 entries，但 entry 仍可能拥有 `id` field，并出现在 response 中。保留 `id` 主要是为了降低从 Strapi 4 迁移到 Strapi 5 的成本。详细变化参阅 [breaking change: use documentId](/cms/migration/v4-to-v5/breaking-changes/use-document-id)。
