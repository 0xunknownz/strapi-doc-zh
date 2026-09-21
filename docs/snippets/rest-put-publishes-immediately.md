# 📖 对照翻译：REST PUT and Draft & Publish

> Source: `docusaurus/docs/snippets/rest-put-publishes-immediately.md`  
> Upstream SHA: `71a20a7cd20f8b9362b48da3d275f98e97a4fc29`

**Original:** With Draft & Publish enabled, a PUT request without a `status` parameter publishes the changes immediately. Pass `?status=draft` to update the draft only. This also applies to single types.

**中文译文:** 启用 Draft & Publish 后，REST `PUT` 如果没有传 `status` parameter，会立即 publish 本次修改。若只希望更新 draft，请传入 `?status=draft`。该规则同样适用于 single types。详见 [REST API: status](/cms/api/rest/status#create-update)。
