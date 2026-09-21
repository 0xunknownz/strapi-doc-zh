# 📖 对照翻译：REST API: Population & Field Selection

> Source: `docusaurus/docs/cms/api/rest/populate-select.md`  
> Upstream SHA: `84982afe08dac15ea9e956df24f73b333f82b6aa`

**Original:** Use the `populate` parameter to include relations, media fields, components, and dynamic zones in REST API responses. Use the `fields` parameter to return only specific fields.

**中文译文:** 使用 `populate` parameter 可以在 REST API response 中包含 relations、media fields、components 与 dynamic zones；使用 `fields` parameter 可以只返回指定 fields。

**Original:** The REST API by default does not populate relations, media fields, components, or dynamic zones. Use `populate` for these fields and `fields` to limit returned scalar fields.

**中文译文:** REST API 默认不会 populate relations、media fields、components 或 dynamic zones。要返回这些内容需使用 `populate`；如果只想返回部分 scalar fields，则使用 `fields`。

## Field selection

**Original:** Queries can accept a `fields` parameter to select only some fields. By default, REST API returns string, date, number, boolean, array, and JSON field types.

**中文译文:** Query 可以通过 `fields` parameter 只选择部分 fields。REST API 默认可直接返回 string、date/time、number、boolean、array、JSON 等 scalar/generic fields。

**Original:**

| Use case | Example parameter syntax |
|---|---|
| Select a single field | `fields=name` |
| Select multiple fields | `fields[0]=name&fields[1]=description` |

**中文译文:**

| 用法 | Parameter 示例 |
|---|---|
| 选择单个 field | `fields=name` |
| 选择多个 fields | `fields[0]=name&fields[1]=description` |

**Original:** Field selection does not work on relational, media, component, or dynamic zone fields. Use `populate` for these.

**中文译文:** `fields` 不能直接选择 relation、media、component 或 dynamic zone fields。要返回这些结构，需要使用 `populate`。

**Original:** Example:

`GET /api/restaurants?fields[0]=name&fields[1]=description`

**中文译文:** 该 request 只返回 restaurant 的 `name` 和 `description` fields（以及 Strapi response 中必要的标识字段）。

```js
const qs = require('qs');
const query = qs.stringify(
  {
    fields: ['name', 'description'],
  },
  {
    encodeValuesOnly: true,
  }
);

await request(`/api/restaurants?${query}`);
```

## Population

**Original:** REST API does not populate any field type by default. Pass `populate` to include relations, media fields, components, or dynamic zones. Populated relations return full objects; REST API currently cannot return only an array of relation IDs.

**中文译文:** REST API 默认不 populate 任何 relation-like field。通过 `populate` 可以返回 relations、media fields、components 与 dynamic zones。被 populate 的 relation 会返回完整 object；当前 REST API 不能只返回 relation IDs 数组。

**Original:** The `find` permission must be enabled for content-types being populated. If the requesting role cannot access a content-type, it will not be populated.

**中文译文:** 被 populate 的 content-type 必须对当前 role 启用 `find` permission。如果 role 无权访问某个 content-type，该内容不会出现在 population 结果中。

**Original:** `populate=deep` plugins are not recommended in Strapi.

**中文译文:** Strapi 官方不建议使用 `populate=deep` 类 plugins。建议显式声明需要 populate 的结构和深度，以便控制性能与 response 大小。

**Original:** Large populate arrays are limited by the query parser `arrayLimit` (default `100`). Raise `arrayLimit` on the `strapi::query` middleware if required; higher values increase parsing cost.

**中文译文:** Query string 中大量 `populate[0]`、`populate[1]` 等 array entries 会受到 query parser 的 `arrayLimit` 限制，默认值为 `100`。如确有需要，可在 `strapi::query` middleware 中提高 `arrayLimit`，但更高值会增加每次 request 的解析成本。

**Original:**

| Use case | Example syntax |
|---|---|
| Populate everything 1 level deep | `populate=*` |
| Populate one relation | `populate=a-relation-name` |
| Populate several relations | `populate[0]=relation-name&populate[1]=another-relation-name` |
| Populate nested relations | `populate[root-relation-name][populate][0]=nested-relation-name` |
| Populate a component | `populate[0]=component-name` |
| Populate a nested component | `populate[0]=component-name&populate[1]=component-name.nested-component-name` |
| Populate a dynamic zone | `populate[0]=dynamic-zone-name` |
| Populate component-specific dynamic-zone content | `populate[dynamic-zone-name][on][component-category.component-name][populate][relation-name][populate][0]=field-name` |

**中文译文:**

| 用法 | Example syntax |
|---|---|
| 1 层 populate 全部可 population 内容 | `populate=*` |
| Populate 一个 relation | `populate=a-relation-name` |
| Populate 多个 relations | `populate[0]=relation-name&populate[1]=another-relation-name` |
| Populate nested relation | `populate[root-relation-name][populate][0]=nested-relation-name` |
| Populate component | `populate[0]=component-name` |
| Populate nested component | `populate[0]=component-name&populate[1]=component-name.nested-component-name` |
| Populate dynamic zone | `populate[0]=dynamic-zone-name` |
| 精细 population dynamic-zone component | `populate[dynamic-zone-name][on][component-category.component-name][populate][relation-name][populate][0]=field-name` |

**Original:** For complex multi-level queries, use the interactive query builder.

**中文译文:** 构建多层 population 等复杂 query 时，建议使用 [interactive query builder](/cms/api/rest/interactive-query-builder)。

### Combining population with other operators

**Original:** `populate` can be combined with field selection, filters, and sort.

**中文译文:** `populate` 可以与 `fields`、`filters`、`sort` 等 operators 组合使用。

**Original:** Top-level pagination works alongside `populate`, but pagination cannot be applied directly to populated relations.

**中文译文:** Top-level `pagination[page]` / `pagination[pageSize]` 可以与 `populate` 同时使用，用于分页主 query 结果；但 REST API **不支持对 populated relation 直接做 nested pagination**。

#### Populate with field selection

**Original:**

`GET /api/articles?fields[0]=title&fields[1]=slug&populate[headerImage][fields][0]=name&populate[headerImage][fields][1]=url`

**中文译文:** 上例同时限制 article 顶层 fields 为 `title`、`slug`，并 populate `headerImage`，但对图片只返回 `name` 与 `url`。

```js
const qs = require('qs');
const query = qs.stringify(
  {
    fields: ['title', 'slug'],
    populate: {
      headerImage: {
        fields: ['name', 'url'],
      },
    },
  },
  {
    encodeValuesOnly: true,
  }
);

await request(`/api/articles?${query}`);
```

#### Populate with filtering

**Original:** `filters`, `sort`, and `populate` can be combined to control which related entries are returned.

**中文译文:** 可以在某个 populated relation 内同时使用 `filters` 与 `sort`，控制返回哪些 related entries 以及排序方式。

```js
const qs = require('qs');
const query = qs.stringify(
  {
    populate: {
      categories: {
        sort: ['name:asc'],
        filters: {
          name: {
            $eq: 'Cars',
          },
        },
      },
    },
  },
  {
    encodeValuesOnly: true,
  }
);

await request(`/api/articles?${query}`);
```

**Original:** For many-to-many and other join-table relations, explicit `sort` inside `populate` overrides the default connect order. Omit `sort` to preserve connect order.

**中文译文:** 对 many-to-many 等使用 join table 的 relations，在 `populate` object 中显式设置 `sort` 会覆盖默认 connect order。如果希望保留 entries 建立关联时的顺序，请不要设置 `sort`。

**Original:** In production, prefer explicit population over `populate=*`, limit depth to 2-3 levels, and consider centralizing population in route middlewares.

**中文译文:** Production 中应优先显式声明 population，而不是使用 `populate=*`；建议将深度控制在 2–3 层，并可考虑在 route middleware 中集中管理 population logic。

**Original:** Empty populated `morphMany` relations return `[]` instead of `null`.

**中文译文:** 被 populate 后，如果 `morphMany` relation 为空（包括 `type: 'media', multiple: true` 等场景），response 返回 `[]` 而不是 `null`，行为与 `oneToMany`、`manyToMany` 一致。
