# 📖 对照翻译：REST API parameters

> Source: `docusaurus/docs/cms/api/rest/parameters.md`  
> Upstream SHA: `041364afb0bd996519bdd8978f93b72aca2d5854`

**Original:** REST API parameters filter, sort, paginate, and select fields and relations in Strapi queries. Use `filters`, `locale`, `populate`, `sort`, and `pagination` to refine your content requests.

**中文译文:** REST API parameters 用于筛选、排序、分页，以及选择 fields / relations。通过 `filters`、`locale`、`populate`、`sort`、`pagination` 等参数，可以精确控制 Content API request。

**Original:** API parameters can filter, sort, paginate results and select fields/relations. Optional Strapi features add parameters such as publication state and locale.

**中文译文:** 通用参数可以控制 filtering、sorting、pagination、field selection 与 relation population；启用 Draft & Publish、Internationalization 等可选功能后，还可以使用 publication status、locale 等额外参数。

**Original:**

| Operator | Type | Description |
|---|---|---|
| `filters` | Object | Filter response |
| `locale` | String | Select locale |
| `status` | String | Select Draft & Publish status |
| `publicationFilter` | String | Select documents by draft/published relationship |
| `populate` | String/Object | Populate relations/components/dynamic zones |
| `fields` | Array | Select fields |
| `sort` | String/Array | Sort response |
| `pagination` | Object | Paginate entries |

**中文译文:**

| Parameter | Type | 中文说明 |
|---|---|---|
| `filters` | Object | [筛选 response](/cms/api/rest/filters) |
| `locale` | String | [选择 locale](/cms/api/rest/locale) |
| `status` | String | [选择 Draft & Publish status](/cms/api/rest/status) |
| `publicationFilter` | String | [按 draft / published 关系筛选 documents](/cms/api/rest/publication-filter) |
| `populate` | String / Object | [Populate relations、components、dynamic zones](/cms/api/rest/populate-select#population) |
| `fields` | Array | [只返回指定 fields](/cms/api/rest/populate-select#field-selection) |
| `sort` | String / Array | [排序 response](/cms/api/rest/sort-pagination#sorting) |
| `pagination` | Object | [分页 entries](/cms/api/rest/sort-pagination#pagination) |

**Original:** Long bracket-encoded lists are limited by `arrayLimit` on `strapi::query`.

**中文译文:** `populate[0]`、`fields[0]` 等较长的 bracket-encoded list 会受到 `strapi::query` middleware 的 `arrayLimit` 限制。需要更长数组时可调整该配置，但解析成本也会增加。

**Original:** Query parameters use LHS bracket syntax with square brackets `[]`.

**中文译文:** REST API query parameters 使用 LHS bracket syntax，也就是通过方括号 `[]` 表达 nested object / array。

**Original:** Use the interactive query builder for long and complex query URLs.

**中文译文:** 多参数组合导致 URL 复杂时，建议使用 [interactive query builder](/cms/api/rest/interactive-query-builder) 辅助生成 query string。
