# 📖 对照翻译：Document Service API: Selecting fields

> Source: `docusaurus/docs/cms/api/document-service/fields.md`  
> Upstream SHA: `0a73926666887164b4d5be72baff31b5ec9454bd`

**Original:** Use the `fields` parameter in Document Service API queries to select specific fields to return with your results, reducing data payload across `findOne()`, `findMany()`, `create()`, `update()`, `delete()`, `publish()`, and other document operations.

**中文译文:** 在 Document Service API query 中使用 `fields` parameter，可以只返回指定 fields，从而减少 response payload。该参数适用于 `findOne()`、`findMany()`、`create()`、`update()`、`delete()`、`publish()` 等 document operations。

**Original:** By default the Document Service API returns all the fields of a document but does not populate any fields. Use `fields` to return only specific fields.

**中文译文:** 默认情况下，Document Service API 会返回 document 的全部普通 fields，但不会自动 populate relation、media、component 或 dynamic zone。可以通过 `fields` 只返回需要的字段。

**Original:** You can also use `populate` to populate relations, media fields, components, or dynamic zones.

**中文译文:** 如果还需要返回 relations、media fields、components 或 dynamic zones，请同时使用 `populate`，详见 [Document Service API: Populate](/cms/api/document-service/populate)。

**Original:** In Strapi 5, entries should generally be targeted by `documentId`, though an `id` field may still be present in responses for Strapi 4 compatibility.

**中文译文:** Strapi 5 中建议使用 `documentId` 定位 entry。为便于从 Strapi 4 迁移，response 中仍可能出现 `id` field。详情参阅 `docs/snippets/id-in-responses.md`。

## Select fields with `findOne()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").findOne({
  documentId: 'a1b2c3d4e5f6g7h8i9j0klm',
  fields: ["name", "description"],
});
```

**中文译文:** 使用 `findOne()` 时，将 `fields` 设置为 `["name", "description"]`，response 只返回指定 fields（以及必要的 document identifier）。

## Select fields with `findFirst()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").findFirst({
  fields: ["name", "description"],
});
```

**中文译文:** `findFirst()` 同样支持 `fields`；上例只返回第一条匹配 document 的 `name` 与 `description`。

## Select fields with `findMany()`

**Original:**
```js
const documents = await strapi.documents("api::restaurant.restaurant").findMany({
  fields: ["name", "description"],
});
```

**中文译文:** `findMany()` 返回多个 documents 时，`fields` 会应用到每一条结果。

## Select fields with `create()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").create({
  data: {
    name: "Restaurant B",
    description: "Description for the restaurant",
  },
  fields: ["name", "description"],
});
```

**中文译文:** `create()` 中的 `fields` 只影响**创建成功后的返回内容**，不会限制 `data` 中可以写入的 fields。

## Select fields with `update()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").update({
  documentId: "fmtr6d7ktzpgrijqaqgr6vxs",
  data: {
    name: "Restaurant C",
  },
  fields: ["name"],
});
```

**中文译文:** `update()` 中可以通过 `fields` 控制 update 完成后 response 中返回哪些 fields。

## Select fields with `delete()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").delete({
  documentId: "fmtr6d7ktzpgrijqaqgr6vxs",
  fields: ["name"],
});
```

**中文译文:** `delete()` 会返回被删除 document 的 versions；`fields` 用于限制这些 returned entries 中包含的 fields。

## Select fields with `publish()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").publish({
  documentId: "fmtr6d7ktzpgrijqaqgr6vxs",
  fields: ["name"],
});
```

**中文译文:** `publish()` 也支持 `fields`。如果一个 document 有多个 locale versions，返回的 published entries 都会按该 fields selection 裁剪。

## Select fields with `unpublish()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").unpublish({
  documentId: "cjld2cjxh0000qzrmn831i7rn",
  fields: ["name"],
});
```

**中文译文:** `unpublish()` 的返回值同样可以通过 `fields` 限制。

## Select fields with `discardDraft()`

**Original:**
```js
const document = await strapi.documents("api::restaurant.restaurant").discardDraft({
  documentId: "fmtr6d7ktzpgrijqaqgr6vxs",
  fields: ["name"],
});
```

**中文译文:** `discardDraft()` 会返回被 discard 的 draft entries；`fields` 决定这些 entries 返回哪些 fields。
