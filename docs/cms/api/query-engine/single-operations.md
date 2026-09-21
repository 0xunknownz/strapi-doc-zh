# 📖 对照翻译：Single Operations with the Query Engine API

> Source: `docusaurus/docs/cms/api/query-engine/single-operations.md`  
> Upstream SHA: `d49c6e12d8008dbdfd49b669df1b6a66e4789421`

**Original:** The Query Engine API provides methods to find, create, update, and delete individual entries with filtering, selection, pagination, and relation population options.

**中文译文:** Query Engine API 提供针对单条 entry 的查询、创建、更新与删除方法，并支持 filtering、field selection、pagination 和 relation population。

**Original:** Only use Query Engine operations when the corresponding Document Service method cannot cover your use case.

**中文译文:** 只有在 Document Service API 对应 method 无法满足需求时，才建议使用 Query Engine。Query Engine 更接近 database layer，不理解完整的 Strapi document 语义。

## `findOne()`

**Original:** Finds the first entry matching the parameters.

Syntax: `findOne(parameters) ⇒ Entry`

**中文译文:** `findOne()` 返回第一个符合条件的 database entry。

语法：`findOne(parameters) ⇒ Entry`

**Original:**

| Parameter | Type | Description |
|---|---|---|
| `select` | String / String[] | Attributes to return |
| `where` | WhereParameter | Filters |
| `offset` | Integer | Number of entries to skip |
| `orderBy` | OrderByParameter | Ordering definition |
| `populate` | PopulateParameter | Relations to populate |

**中文译文:**

| Parameter | 类型 | 说明 |
|---|---|---|
| `select` | String / String[] | 要返回的 attributes |
| `where` | WhereParameter | 查询 filters |
| `offset` | Integer | 跳过的 entries 数量 |
| `orderBy` | OrderByParameter | 排序定义 |
| `populate` | PopulateParameter | 需要 populate 的 relations |

**Original code (kept unchanged):**

```js
const entry = await strapi.db.query('api::blog.article').findOne({
  select: ['title', 'description'],
  where: { title: 'Hello World' },
  populate: { category: true },
});
```

**中文译文:** 上例只返回 `title` 和 `description`，筛选 title 为 `Hello World` 的第一条 row，并 populate `category`。

## `findMany()`

**Original:** Finds entries matching the parameters.

Syntax: `findMany(parameters) ⇒ Entry[]`

**中文译文:** `findMany()` 返回所有符合条件的 entries。

语法：`findMany(parameters) ⇒ Entry[]`

**Original:**

| Parameter | Description |
|---|---|
| `select` | Attributes to return |
| `where` | Filters |
| `limit` | Number of entries to return |
| `offset` | Number of entries to skip |
| `orderBy` | Ordering definition |
| `populate` | Relations to populate |

**中文译文:**

| Parameter | 说明 |
|---|---|
| `select` | 要返回的 attributes |
| `where` | Filters |
| `limit` | 最多返回 entries 数量 |
| `offset` | 跳过 entries 数量 |
| `orderBy` | 排序定义 |
| `populate` | 需要 populate 的 relations |

```js
const entries = await strapi.db.query('api::blog.article').findMany({
  select: ['title', 'description'],
  where: { title: 'Hello World' },
  orderBy: { publishedAt: 'DESC' },
  populate: { category: true },
});
```

**中文译文:** 示例按 `publishedAt` descending 排序，并 populate `category`。代码保持原样。

## `findWithCount()`

**Original:** Finds and counts entries matching the parameters.

Syntax: `findWithCount(parameters) => [Entry[], number]`

**中文译文:** `findWithCount()` 在返回匹配 entries 的同时返回总数量。

语法：`findWithCount(parameters) => [Entry[], number]`

```js
const [entries, count] = await strapi.db.query('api::blog.article').findWithCount({
  select: ['title', 'description'],
  where: { title: 'Hello World' },
  orderBy: { title: 'DESC' },
  populate: { category: true },
});
```

**中文译文:** 返回值是二元数组：第一项为 entries，第二项为匹配总数 `count`。

## `create()`

**Original:** Creates one entry and returns it.

Syntax: `create(parameters) => Entry`

**中文译文:** `create()` 创建一条 database entry 并返回该 entry。

**Original:** Parameters are `select`, `populate`, and `data`.

**中文译文:** 常用 parameters：
- `data`：要写入的数据；
- `select`：限制返回 attributes；
- `populate`：在 response 中加载 relations。

```js
const entry = await strapi.db.query('api::blog.article').create({
  data: {
    title: 'My Article',
  },
});
```

## `update()`

**Original:** Updates one entry and returns it.

Syntax: `update(parameters) => Entry`

**中文译文:** `update()` 更新第一条符合 `where` 条件的 entry，并返回更新后的结果。

```js
const entry = await strapi.db.query('api::blog.article').update({
  where: { id: 1 },
  data: {
    title: 'xxx',
  },
});
```

**Original:** Parameters include `select`, `populate`, `where`, and `data`.

**中文译文:** 可使用 `where` 定位 database row，通过 `data` 写入修改，同时用 `select` / `populate` 控制返回内容。

## `delete()`

**Original:** Deletes one entry and returns it.

Syntax: `delete(parameters) => Entry`

**中文译文:** `delete()` 删除一条匹配 entry，并返回被删除的 entry。

```js
const entry = await strapi.db.query('api::blog.article').delete({
  where: { id: 1 },
});
```

**中文译文:** Query Engine 使用 database `id` 与 row-level 条件。对于 Strapi 5 的正常内容操作，应优先使用 Document Service API 的 `documentId`。
