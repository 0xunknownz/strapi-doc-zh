# 📖 对照翻译：REST API: Sort & Pagination

> Source: `docusaurus/docs/cms/api/rest/sort-pagination.md`  
> Upstream SHA: `2e51a6b42f2db0b0fcd7451b07cbe86d79bcd6a1`

**Original:** Sort REST API results on one or multiple fields with `:asc` or `:desc` syntax, and paginate using either page-based or offset-based parameters.

**中文译文:** REST API 支持按一个或多个 fields 排序，可使用 `:asc` / `:desc` 指定顺序；分页则可以选择 page-based 或 offset-based 两种模式。

**Original:** Entries returned by REST API queries can be sorted and paginated.

**中文译文:** REST API query 返回的 entries 可以同时应用 sorting 与 pagination。

## Sorting

**Original:** Queries accept a `sort` parameter:
- `GET /api/:pluralApiId?sort=value` for one field
- `GET /api/:pluralApiId?sort[0]=value1&sort[1]=value2` for multiple fields

**中文译文:** Query 支持 `sort` parameter：
- 单 field：`GET /api/:pluralApiId?sort=value`
- 多 fields：`GET /api/:pluralApiId?sort[0]=value1&sort[1]=value2`

**Original:** Use `:asc` for ascending order (default and can be omitted) and `:desc` for descending order.

**中文译文:** 使用 `:asc` 表示 ascending order；它是默认值，因此可以省略。使用 `:desc` 表示 descending order。

### Example: Sort using 2 fields

**Original:** `GET /api/restaurants?sort[0]=Description&sort[1]=Name`

**中文译文:** 该 query 先按 `Description`，再按 `Name` 排序；两个 field 都使用默认 ascending order。

```js
const qs = require('qs');
const query = qs.stringify({
  sort: ['Description', 'Name'],
}, {
  encodeValuesOnly: true,
});

await request(`/api/restaurants?${query}`);
```

### Example: Sort using 2 fields and set the order

**Original:** `GET /api/restaurants?sort[0]=Description:asc&sort[1]=Name:desc`

**中文译文:** 该 query 将 `Description` 按 ascending 排序，同时将 `Name` 按 descending 排序。

```js
const qs = require('qs');
const query = qs.stringify({
  sort: ['Description:asc', 'Name:desc'],
}, {
  encodeValuesOnly: true,
});

await request(`/api/restaurants?${query}`);
```

## Pagination

**Original:** Results can be paginated either by page or by offset. Pagination methods cannot be mixed.

**中文译文:** REST API 支持两种 pagination：
- 按 page：指定 page number 与每页 entries 数量；
- 按 offset：指定跳过多少 entries，以及返回多少 entries。

两种模式**不能混用**：必须选择 `page/pageSize` 或 `start/limit` 其中一套。

### Pagination by page

**Original:**

| Parameter | Type | Description | Default |
|---|---|---|---|
| `pagination[page]` | Integer | Page number | 1 |
| `pagination[pageSize]` | Integer | Page size | 25 |
| `pagination[withCount]` | Boolean | Include total entries and page count | true |

**中文译文:**

| Parameter | 类型 | 说明 | 默认值 |
|---|---|---|---|
| `pagination[page]` | Integer | 页码 | 1 |
| `pagination[pageSize]` | Integer | 每页 entries 数量 | 25 |
| `pagination[withCount]` | Boolean | 是否返回总 entries 数与 page count | true |

**Original:** Example:

`GET /api/articles?pagination[page]=1&pagination[pageSize]=10`

**中文译文:** 示例请求第 1 页，每页 10 条。Response 的 `meta.pagination` 会包含 `page`、`pageSize`、`pageCount` 与 `total`。

```js
const qs = require('qs');
const query = qs.stringify({
  pagination: {
    page: 1,
    pageSize: 10,
  },
}, {
  encodeValuesOnly: true,
});

await request(`/api/articles?${query}`);
```

### Pagination by offset

**Original:**

| Parameter | Type | Description | Default |
|---|---|---|---|
| `pagination[start]` | Integer | Number of entries to skip | 0 |
| `pagination[limit]` | Integer | Number of entries to return | 25 |
| `pagination[withCount]` | Boolean | Include total number of entries | true |

**中文译文:**

| Parameter | 类型 | 说明 | 默认值 |
|---|---|---|---|
| `pagination[start]` | Integer | 跳过的 entries 数量 | 0 |
| `pagination[limit]` | Integer | 最多返回的 entries 数量 | 25 |
| `pagination[withCount]` | Boolean | 是否返回总 entries 数量 | true |

**Original:** The default and maximum values for `pagination[limit]` are configurable with `api.rest.defaultLimit` and `api.rest.maxLimit`.

**中文译文:** `pagination[limit]` 的默认值和最大值可以在 `./config/api.js` 中通过 `api.rest.defaultLimit` 与 `api.rest.maxLimit` 配置。

**Original:** Example:

`GET /api/articles?pagination[start]=0&pagination[limit]=10`

**中文译文:** 示例从 offset 0 开始，最多返回 10 条 entries。Offset pagination 的 response 会在 `meta.pagination` 中返回 `start`、`limit` 和（默认情况下）`total`。

```js
const qs = require('qs');
const query = qs.stringify({
  pagination: {
    start: 0,
    limit: 10,
  },
}, {
  encodeValuesOnly: true,
});

await request(`/api/articles?${query}`);
```
