# 📖 对照翻译：Ordering and Paginating with the Entity Service API

> Source: `docusaurus/docs/cms/api/entity-service/order-pagination.md`  
> Upstream SHA: `0b37a5b8482919eb165642bd902a373741fc8e03`

**Original:** Order and paginate Entity Service API results using `sort`, `start`/`limit`, or `page`/`pageSize`.

**中文译文:** Entity Service API 的 `findMany()` 支持通过 `sort` 排序，并可以使用 `start` / `limit` 或 `page` / `pageSize` 分页。

**Original:** Entity Service is deprecated in Strapi 5.

**中文译文:** Entity Service 在 Strapi 5 中已 deprecated；新代码应使用 Document Service API。

## Ordering

### Single field

```js
strapi.entityService.findMany('api::article.article', {
  sort: 'id',
});

strapi.entityService.findMany('api::article.article', {
  sort: { id: 'desc' },
});
```

**中文译文:** String form 使用默认 ascending；object form 可以显式指定 `asc` / `desc`。

### Multiple fields

```js
strapi.entityService.findMany('api::article.article', {
  sort: ['publishDate', 'name'],
});

strapi.entityService.findMany('api::article.article', {
  sort: [
    { title: 'asc' },
    { publishedAt: 'desc' },
  ],
});
```

**中文译文:** 多字段排序可以使用 string array，或 object array 为每个 field 指定方向。

### Relational ordering

```js
strapi.entityService.findMany('api::article.article', {
  sort: {
    author: {
      name: 'asc',
    },
  },
});
```

**中文译文:** 也可以按 related entity 的 attribute 排序，例如 `author.name`。

## Pagination

**Original:** Offset pagination:

```js
strapi.entityService.findMany('api::article.article', {
  start: 10,
  limit: 15,
});
```

**中文译文:** `start` 表示跳过 entries 数量，`limit` 表示最多返回数量。

**Original:** Page pagination:

```js
strapi.entityService.findMany('api::article.article', {
  page: 1,
  pageSize: 15,
});
```

**中文译文:** 也可以使用 `page` 与 `pageSize` 进行页码式分页。
