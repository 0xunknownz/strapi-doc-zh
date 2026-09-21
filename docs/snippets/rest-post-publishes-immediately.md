# 📖 对照翻译：REST POST and Draft & Publish

> Source: `docusaurus/docs/snippets/rest-post-publishes-immediately.md`  
> Upstream SHA: `aeab29a3cd3c9677d7b75fca77a59fcbf5f9e514`

**Original:** With Draft & Publish enabled, a POST request without a `status` parameter creates the document and publishes it immediately. Pass `?status=draft` to create it as a draft.

**中文译文:** 启用 Draft & Publish 后，REST `POST` 如果没有传 `status` parameter，会创建 document 并立即 publish。若要只创建 draft，请传入 `?status=draft`。详见 [REST API: status](/cms/api/rest/status#create-update)。
