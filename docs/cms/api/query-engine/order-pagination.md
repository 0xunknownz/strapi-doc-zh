# 📖 对照翻译：Ordering and Paginating with the Query Engine API

> Source: `docusaurus/docs/cms/api/query-engine/order-pagination.md`  
> Upstream SHA: `2427dd992aefecba3f1c0dc1aede076cad5178ad`

**Original:** The Query Engine API supports ordering results with the `orderBy` parameter on single or multiple attributes, including relational ordering, and pagination with `offset` and `limit`.

**中文译文:** Query Engine API 使用 `orderBy` 对单个或多个 attributes 排序，也支持 relational ordering；分页则使用 `offset` 与 `limit`。

## Ordering

**Original:** Order results using `orderBy`.

**中文译文:** 在 `findMany()` 等 query 中传入 `orderBy` 即可排序。

### Single

```js
strapi.db.query('api::article.article').findMany({
  orderBy: 'id',
});

strapi.db.query('api::article.article').findMany({
  orderBy: { id: 'asc' },
});
```

**中文译文:** 单 field 可以直接传 attribute name，也可以通过 object 指定 `asc` / `desc`。

### Multiple

```js
strapi.db.query('api::article.article').findMany({
  orderBy: ['id', 'name'],
});

strapi.db.query('api::article.article').findMany({
  orderBy: [{ title: 'asc' }, { publishedAt: 'desc' }],
});
```

**中文译文:** 多字段可以传入 array；如需为各 field 指定不同方向，则使用 object array。

### Relational ordering

```js
strapi.db.query('api::article.article').findMany({
  orderBy: {
    author: {
      name: 'asc',
    },
  },
});
```

**中文译文:** Query Engine 还支持按 relation 内部 attribute 排序。上例根据 `author.name` ascending 排序。

## Pagination

**Original:** Use `offset` and `limit`.

```js
strapi.db.query('api::article.article').findMany({
  offset: 15,
  limit: 10,
});
```

**中文译文:** `offset` 表示跳过多少 entries，`limit` 表示最多返回多少 entries。上例跳过前 15 条，最多返回 10 条。
