# 📖 对照翻译：Bulk Operations with the Query Engine API

> Source: `docusaurus/docs/cms/api/query-engine/bulk-operations.md`  
> Upstream SHA: `a43116d67e113273c1d6932c00d87fa7b29e955b`

**Original:** Bulk Operations with the Query Engine API enable you to create, update, delete, and count multiple entries at once using `createMany()`, `updateMany()`, `deleteMany()`, and `count()`.

**中文译文:** Query Engine API 的 Bulk Operations 可通过 `createMany()`、`updateMany()`、`deleteMany()` 和 `count()` 一次处理多条 database entries。

**Original:** To avoid performance issues, bulk operations are not allowed on relations.

**中文译文:** 为避免性能问题，bulk operations **不支持直接操作 relations**。

## `createMany()`

**Original:** Creates multiple entries.

Syntax: `createMany(parameters) => { count: number, ids: id[] }`

**中文译文:** `createMany()` 一次创建多条 entries。

语法：`createMany(parameters) => { count: number, ids: id[] }`

**Original:** The `data` parameter is an array of input objects.

**中文译文:** `data` 是 input object array，每个 object 对应一条新 entry。

```js
await strapi.db.query("api::blog.article").createMany({
  data: [
    { title: "ABCD" },
    { title: "EFGH" },
  ],
});

// { count: 2 , ids: [1,2]}
```

**Original:** MySQL only returns one id containing the last inserted id. Before Strapi v4.9.0, `createMany()` returned only `count`.

**中文译文:** MySQL 下 `ids` 只会包含一个值，即最后插入 row 的 id。Strapi v4.9.0 之前，`createMany()` 只返回 `count`。

## `updateMany()`

**Original:** Updates multiple entries matching the parameters.

Syntax: `updateMany(parameters) => { count: number }`

**中文译文:** `updateMany()` 更新所有符合 `where` 条件的 entries，并返回受影响数量。

```js
await strapi.db.query("api::shop.article").updateMany({
  where: {
    price: 20,
  },
  data: {
    price: 18,
  },
});

// { count: 42 }
```

**中文译文:** 上例将所有 `price = 20` 的 rows 更新为 `18`。

## `deleteMany()`

**Original:** Deletes multiple entries matching the parameters.

Syntax: `deleteMany(parameters) => { count: number }`

**中文译文:** `deleteMany()` 删除全部匹配 `where` 的 entries，并返回删除数量。

```js
await strapi.db.query("api::blog.article").deleteMany({
  where: {
    title: {
      $startsWith: "v3",
    },
  },
});

// { count: 42 }
```

## Aggregations — `count()`

**Original:** Counts entries matching the parameters.

Syntax: `count(parameters) => number`

**中文译文:** `count()` 统计符合 `where` 条件的 database entries 数量。

```js
const count = await strapi.db.query("api::blog.article").count({
  where: {
    title: {
      $startsWith: "v3",
    },
  },
});

// 12
```
