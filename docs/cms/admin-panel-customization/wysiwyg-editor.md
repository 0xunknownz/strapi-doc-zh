# 📖 对照翻译：Change the default rich text editor

> Source: `docusaurus/docs/cms/admin-panel-customization/wysiwyg-editor.md`  
> Upstream SHA: `596a9b6366ea5aec168514269413a338eeeddfb8`

**Original:** Strapi admin panel includes a built-in WYSIWYG markdown editor for `richtext` fields. Replace it with Marketplace plugins or a custom field.

**中文译文:** Strapi admin panel 为 `richtext` field 内置 WYSIWYG Markdown editor。可以通过 Marketplace plugin 替换，也可以开发 custom field 实现更深度的 editor integration。

**Original:** This page covers the WYSIWYG Markdown editor for `richtext`, not the JSON-based Blocks field.

**中文译文:** 本页讨论的是 `richtext` 使用的 WYSIWYG Markdown editor；如果使用 JSON-based **Blocks** field，请参阅 Content Manager API 的 `addRichTextBlocks`。

**Original:** Option 1: install a third-party editor plugin, e.g. CKEditor, from Marketplace.

**中文译文:** 方案 1：从 [Strapi Marketplace](https://community.strapi.io/marketplace) 安装第三方 editor plugin，例如 CKEditor integration。适合快速试用和标准化需求。

**Original:** Option 2: create your own plugin/custom field for a fully custom WYSIWYG editor.

**中文译文:** 方案 2：开发自己的 plugin，并注册 [custom field](/cms/features/custom-fields)，实现完整自定义 WYSIWYG。适合需要定制 schema、validation、toolbar behavior 等深度集成场景。

**Original:** Start with a Marketplace plugin, then move to a custom field if deeper integration is needed.

**中文译文:** 推荐先用 Marketplace plugin 验证需求；只有在标准 plugin 无法满足时，再投入 custom field development。
