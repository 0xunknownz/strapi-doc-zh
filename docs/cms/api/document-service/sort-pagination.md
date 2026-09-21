# 📖 对照翻译：Document Service API: Sorting and paginating results

> Source: `docusaurus/docs/cms/api/document-service/sort-pagination.md`  
> Upstream SHA: `7d37e19822feed1a2fd9f7edfa6a4b63fc0d8dfd`

**Original:** Use the Document Service API's `sort` and pagination parameters to order query results by single or multiple fields and control result limits with `limit` and `start`.

**中文译文:** Document Service API 支持使用 `sort` 对 query results 按一个或多个 fields 排序，并通过 `limit` 与 `start` 控制 pagination 范围。

**Original:** The Document Service API offers the ability to sort and paginate query results.

**中文译文:** Document Service API 的 `findMany()` 等查询方法支持 sorting 与 pagination。

## Sort

**Original:** To sort results returned by the Document Service API, include the `sort` parameter.

**中文译文:** 若要排序 Document Service API 返回的结果，请在 query parameters 中加入 `sort`。

### Sort on a single field

**Original:**
```js
const documents = await strapi.documents("api::article.article").findMany({
  sort: "title:asc",
});
```

**中文译文:** 上例按 `title` ascending 排序。Single-field sort 可以直接使用 `"field:asc"` 或 `"field:desc"` string。

### Sort on multiple fields

**Original:**
```js
const documents = await strapi.documents("api::article.article").findMany({
  sort: [{ title: "asc" }, { slug: "desc" }],
});
```

**中文译文:** 多字段排序可以传入 sort object array。上例先按 `title` ascending，再按 `slug` descending 排序。

## Pagination

**Original:** Paginate results using the `limit` and `start` parameters.

```js
const documents = await strapi.documents("api::article.article").findMany({
  limit: 10,
  start: 0,
});
```

**中文译文:** Document Service API 使用 offset-based pagination：
- `start`：从第几条记录开始；
- `limit`：最多返回多少条。

上例从第 0 条开始，最多返回 10 个 documents。
