# 📖 对照翻译：Build your query URL with Strapi's interactive tool

> Source: `docusaurus/docs/cms/api/rest/interactive-query-builder.md`  
> Upstream SHA: `be7982a29bd677f600b9056cd193b34bf4342c30`

**Original:** An interactive query builder tool automatically generates REST API query URLs from your endpoint and parameters, powered by the `qs` library to handle complex nested queries.

**中文译文:** Strapi 提供 interactive query builder，可以根据 endpoint 与 parameters 自动生成 REST API query URL。该工具底层基于 `qs` library，适合处理复杂 nested query。

**Original:** REST API parameters can be combined in ways that produce long and complex query URLs.

**中文译文:** REST API 支持大量 parameters 组合，手工构建时 query URL 很容易变得很长且难以维护。

**Original:** Strapi uses the `qs` library to parse and stringify nested JavaScript objects. Use `qs` directly instead of manually creating complex URLs.

**中文译文:** Strapi codebase 使用 `qs` library 解析与 stringify nested JavaScript objects。程序中建议直接用 `qs` 生成复杂 URL，而不是手工拼接。

**Original:** To use the interactive query builder:
1. Replace the Endpoint and Endpoint Query Parameters values.
2. Click **Copy to clipboard** to copy the generated Query String URL.

**中文译文:** 使用 interactive query builder：
1. 在 *Endpoint* 与 *Endpoint Query Parameters* 中填写实际需求；
2. 工具会实时更新 *Query String URL*，点击 **Copy to clipboard** 即可复制。

**Original:** Refer to the REST API parameters table for details about each parameter.

**中文译文:** 各 parameter 的含义与用法请参阅 [REST API parameters](/cms/api/rest/parameters) 以及对应参数的独立文档页。

**Original:** Example input object:

```js
{
  sort: ['title:asc'],
  filters: {
    title: {
      $eq: 'hello',
    },
  },
  populate: {
    author: {
      fields: ['firstName', 'lastName']
    }
  },
  fields: ['title'],
  pagination: {
    pageSize: 10,
    page: 1,
  },
  status: 'published',
  locale: ['en'],
}
```

**中文译文:** 示例同时使用 sorting、filters、populate、fields、pagination、status 和 locale，展示复杂 query object 如何转换为 bracket-encoded query URL。

**Original:** The default endpoint prefix is `/api/`. Keep it unless you changed `rest.prefix`.

**中文译文:** 默认 REST endpoint path 以 `/api/` 开头。除非在 API configuration 中修改了 `rest.prefix`，否则应保持该前缀。例如 books collection type 使用 `/api/books`。

**Original:** The `qs` library and query builder might not detect every syntax error, do not know which parameters/values exist in your project, and provide no autocomplete. A generated URL does not guarantee valid API results.

**中文译文:** 注意该工具只负责把 JavaScript object 转换成 inline query string：
- 不保证发现所有 syntax errors；
- 不知道当前 Strapi 项目实际有哪些 parameters / values；
- 不提供 autocomplete；
- URL 能成功生成，并不代表对应 API request 一定能得到有效结果。
