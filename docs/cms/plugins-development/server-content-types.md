# 📖 对照翻译：Server API — Content-types

> Source: `docusaurus/docs/cms/plugins-development/server-content-types.md`  
> Upstream SHA: `c1c2a455f95ac615bd76d2eb03b24510c2b395ff`

**Original:** A plugin exports a `contentTypes` object to declare plugin content-types. Keep the export key aligned with `info.singularName` so runtime UIDs remain predictable.

**中文译文:** Plugin 可以通过 Server API 的 `contentTypes` object 声明自己的 content-types。推荐让 export key 与 schema 的 `info.singularName` 完全一致，这样 runtime UID 清晰、稳定、易于维护。

## Declaration

**Original:** Each `contentTypes` key registers a content-type under the plugin namespace, and its value contains a `schema`.

**中文译文:** `contentTypes` 中的每个 key 都会在 plugin namespace 下注册一个 content-type，其 value 需要包含 `schema`。

**Original code (kept unchanged):**

```js title="/src/plugins/my-plugin/server/src/content-types/index.js"
'use strict';

const article = require('./article');

module.exports = {
  article: { schema: article },
};
```

```json title="/src/plugins/my-plugin/server/src/content-types/article/schema.json"
{
  "kind": "collectionType",
  "collectionName": "my_plugin_articles",
  "info": {
    "singularName": "article",
    "pluralName": "articles",
    "displayName": "Article"
  },
  "options": {
    "draftAndPublish": false
  },
  "attributes": {
    "title": {
      "type": "string",
      "required": true
    },
    "body": {
      "type": "richtext"
    }
  }
}
```

**中文译文:** 上例 export key 与 `singularName` 都是 `article`，因此 runtime UID 可预测为 `plugin::my-plugin.article`。

## UIDs and naming

**Original:** Plugin content-type UIDs are built as `plugin::<plugin-name>.<content-types-key>`.

**中文译文:** Plugin content-type UID 规则为：

`plugin::<plugin-name>.<content-types-key>`

推荐 `content-types-key === info.singularName`。

| 场景 | 示例 |
|---|---|
| Document Service | `strapi.documents('plugin::my-plugin.article').findMany()` |
| 获取 schema | `strapi.contentType('plugin::my-plugin.article')` |
| Plugin route handler | `handler: 'article.find'` |
| Sanitization | 将该 schema 传给 `strapi.contentAPI.sanitize.output()` |

**Original:** If the export key and `singularName` differ, runtime getters and queries use the export key, not `singularName`.

**中文译文:** 如果两者不一致，runtime UID 会根据 `contentTypes` export key 生成，而不是根据 `singularName`。虽然可能仍能注册成功，但会造成命名混乱，因此不推荐。

## Querying with Document Service

**Original code (kept unchanged):**

```js
module.exports = ({ strapi }) => ({
  async findAll(params = {}) {
    return strapi
      .documents('plugin::my-plugin.article')
      .findMany(params);
  },

  async create(data) {
    return strapi
      .documents('plugin::my-plugin.article')
      .create({ data });
  },
});
```

**中文译文:** Plugin content-type 与 application content-type 一样，可以直接通过 Document Service API 进行 CRUD。

## Accessing the schema

```js
const schema =
  strapi.contentType('plugin::my-plugin.article');

const sanitizedOutput =
  await strapi.contentAPI.sanitize.output(
    data,
    schema,
    { auth: ctx.state.auth }
  );
```

**中文译文:** 获取 schema 后，可以用于 permission-aware sanitization 等场景。

## Best practices

**中文译文:**
- Export key 与 `info.singularName` 保持一致；
- `collectionName` 建议带 plugin prefix，例如 `my_plugin_articles`，避免 table collision；
- 每个 content-type 使用独立 `schema.json`；
- 只有确实需要 publication workflow 时才启用 Draft & Publish，避免给 plugin data model 增加不必要复杂度。
