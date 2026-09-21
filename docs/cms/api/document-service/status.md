# 📖 对照翻译：Document Service API: Usage with Draft & Publish

> Source: `docusaurus/docs/cms/api/document-service/status.md`  
> Upstream SHA: `4ead46097d0cd489f086d82b106e1c425b629b94`

**Original:** Use the `status` parameter with the Document Service API to retrieve published or draft versions of documents, count documents by status, and directly publish documents during creation or updates.

**中文译文:** 使用 Document Service API 的 `status` parameter，可以读取 document 的 published / draft version、按 status 统计 documents，还可以在 create 或 update 时直接 publish。

**Original:** By default the Document Service API returns the draft version when Draft & Publish is enabled.

**中文译文:** Content-type 启用 Draft & Publish 后，Document Service API **默认返回 draft version**。

**Original:** Passing `{ status: 'draft' }` returns the same results as omitting `status`.

**中文译文:** 显式传入 `{ status: 'draft' }` 与完全不传 `status` 的结果相同。

**Original:** Document Service defaults to `draft`, while REST API defaults to `published`.

**中文译文:** 这一点与 REST API 相反：Document Service API 默认 `draft`，REST API 默认 `published`。因此 REST 的 `POST` / `PUT` 不指定 `status` 时会立即 publish。

**Original:** To query documents by how draft and published versions relate, use `publicationFilter`.

**中文译文:** 如果要按 draft / published 的关系筛选 never-published、modified 等 documents，请使用 [`publicationFilter`](/cms/api/document-service/publication-filter)。

## Get published version with `findOne()`

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').findOne({
  documentId: 'a1b2c3d4e5f6g7h8i9j0klm',
  status: 'published'
});
```

**中文译文:** 在 `findOne()` 中传入 `status: 'published'`，返回指定 document 的 published version。

## Get published version with `findFirst()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").findFirst({
  status: 'published',
});
```

**中文译文:** `findFirst()` 中使用 `status: 'published'`，返回第一条匹配 document 的 published version。

## Get published versions with `findMany()`

**Original:**
```js
const documents = await strapi.documents("api::restaurant.restaurant").findMany({
  status: 'published'
});
```

**中文译文:** `findMany()` 中使用 `status: 'published'`，只返回匹配 documents 的 published versions。

## `count()` draft or published versions

**Original:**
```js
const draftsCount = await strapi.documents("api::restaurant.restaurant").count({
  status: 'draft'
});

const publishedCount = await strapi.documents("api::restaurant.restaurant").count({
  status: 'published'
});
```

**中文译文:** `count({ status: 'published' })` 只统计已 publish 的 documents。由于每个 published document 必然仍保留 draft counterpart，`count({ status: 'draft' })` 实际上会统计所有符合其他条件的 documents。

**Original:** To count only never-published drafts, use `publicationFilter` such as `'never-published'` or `'never-published-document'`.

**中文译文:** 如果只想统计从未 publish 的 draft，应使用 `publicationFilter`，例如 `'never-published'` 或 `'never-published-document'`。

## Create and publish

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').create({
  data: {
    name: "New Restaurant",
  },
  status: 'published',
})
```

**中文译文:** `create()` 默认创建 draft；若传入 `status: 'published'`，则创建后立即 publish。

## Update and publish

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').update({
  documentId: 'a1b2c3d4e5f6g7h8i9j0klm',
  data: {
    name: "Biscotte Restaurant (closed)",
  },
  status: 'published',
})
```

**中文译文:** `update()` 默认只更新 draft。传入 `status: 'published'` 后，会更新 draft 并立即 publish 新版本。
