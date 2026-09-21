# 📖 对照翻译：REST API: `publicationFilter`

> Source: `docusaurus/docs/cms/api/rest/publication-filter.md`  
> Upstream SHA: `c9bdc8860b40e8f42fb80528316cec870ebc7f62`

**Original:** Add the optional `publicationFilter` query parameter to query documents by the relationship between their draft and published versions, for example documents that were never published, or documents modified since they were last published. It combines with other query parameters, and `status` still decides whether you get the draft or published version.

**中文译文:** 可选的 `publicationFilter` query parameter 根据 document 的 draft / published versions 之间的关系筛选 documents，例如从未发布过的 document，或自上次 publish 之后 draft 又发生修改的 document。`publicationFilter` 可以与其他 query parameters 组合，而最终返回 draft 还是 published version 仍由 `status` 决定。

**Original:** `status` answers “which version do I want?”, while `publicationFilter` answers “which documents do I want based on how their versions relate?”

**中文译文:** 两个参数解决的问题不同：
- `status`：**返回哪个 version？** draft 还是 published；
- `publicationFilter`：**筛选哪些 documents？** 根据 draft 与 published 的关系筛选。

**Original:** The underlying model is shared with Document Service API `publicationFilter`.

**中文译文:** 这一逻辑由 back-end 的 Document Service API publication model 实现，因此 REST 与 [Document Service publicationFilter](/cms/api/document-service/publication-filter) 的概念一致。

**Original:** Draft & Publish must be enabled. Otherwise `publicationFilter` has no effect.

**中文译文:** Content-type 必须启用 Draft & Publish；如果未启用，`publicationFilter` 不产生效果。

## Available values

| Value | Original meaning | 中文说明 |
|---|---|---|
| `never-published` | Never published in a given locale | 当前 locale 从未 publish |
| `never-published-document` | Never published in any locale | 整个 document 的任何 locale 都从未 publish |
| `modified` | Draft edited since last publication | Draft 自上次 publish 后又有修改 |
| `unmodified` | Draft unchanged since last publication | Draft 与最近一次 published content 一致 |
| `has-published-version` | Both draft and published version exist | 当前 locale 同时存在 draft 与 published |
| `published-without-draft` | Published with no draft counterpart | Published row 没有 draft counterpart，仅用于 diagnostics |
| `published-with-draft` | Published with a draft | Published row 同时有 draft，仅用于 diagnostics |
| `has-published-version-document` | Published in at least one locale | Document 至少有一个 locale 已 publish |

**Original:** Unknown values return HTTP 400.

**中文译文:** 传入未知 `publicationFilter` value 会返回 HTTP `400`。

**Original:** Values ending in `-document` consider all locales; other values work per locale.

**中文译文:** 以 `-document` 结尾的 values 会从整个 document 的所有 locales 角度判断；其他 values 则以单个 locale 为单位判断。未启用 i18n 时两种范围的结果通常等价。

**Original:** REST defaults to `status=published`, so draft-only values such as `never-published` require explicit `status=draft`. Document Service defaults to draft.

**中文译文:** REST API 默认 `status=published`，因此 `never-published` 这类只可能存在 draft 的查询必须显式传 `status=draft`。Document Service API 则默认 draft。

## Common combinations

| Goal | `status` | `publicationFilter` |
|---|---|---|
| Never-published drafts in current locale | `draft` | `never-published` |
| Documents never published in any locale | `draft` | `never-published-document` |
| Modified documents | `draft` or `published` | `modified` |
| Unmodified documents | `draft` or `published` | `unmodified` |
| Has published version in current locale | `draft` or `published` | `has-published-version` |
| Published in at least one locale | `draft` or `published` | `has-published-version-document` |

**中文译文:** 上表展示常见组合。`publicationFilter` 先决定 document group，再由 `status` 决定返回这个 group 的 draft 或 published representation。

**Original:** Opposite status combinations are valid but can return an empty result instead of an error; e.g. `never-published` with `status=published` returns nothing.

**中文译文:** 将某个 filter 与逻辑上不可能存在的 opposite status 组合不会报参数错误，而是返回空结果。例如 never-published document 没有 published version，因此 `publicationFilter=never-published&status=published` 返回空数组。

## Find never-published drafts

**Original:** Use `status=draft&publicationFilter=never-published` for drafts never published in their current locale.

```bash
curl 'http://localhost:1337/api/restaurants?status=draft&publicationFilter=never-published' \
  -H 'Authorization: Bearer <token>'
```

```js
const qs = require('qs');
const query = qs.stringify({
  status: 'draft',
  publicationFilter: 'never-published',
}, {
  encodeValuesOnly: true,
});

await request(`/api/restaurants?${query}`);
```

**中文译文:** 该组合按**当前 locale**判断，返回从未 publish 的 draft。若要跨所有 locales 判断，请使用 `never-published-document`。

## Never published in any locale

**Original:** `never-published-document` considers the whole document. As soon as one locale is published, the entire document is excluded.

```bash
curl 'http://localhost:1337/api/restaurants?status=draft&publicationFilter=never-published-document' \
  -H 'Authorization: Bearer <token>'
```

**中文译文:** `never-published-document` 从整个 document 维度判断。只要其中任意一个 locale 曾 publish，该 document 就不再匹配，即使其他 locale 仍只有 draft。

## Find modified documents

**Original:** `publicationFilter=modified` selects documents whose draft has unpublished changes. `status=draft` returns draft content; REST default `status=published` returns the currently live content of the same documents.

```bash
# Return modified drafts
curl 'http://localhost:1337/api/restaurants?status=draft&publicationFilter=modified' \
  -H 'Authorization: Bearer <token>'

# Return currently live versions of those modified documents
curl 'http://localhost:1337/api/restaurants?publicationFilter=modified' \
  -H 'Authorization: Bearer <token>'
```

**中文译文:** 同一个 `modified` group 可以通过 `status` 查看两种视角：
- `status=draft`：返回尚未发布的新修改；
- 默认 published：返回这些 documents 当前线上仍在使用的旧 published version。

## Find unmodified documents

**Original:** `publicationFilter=unmodified` selects documents whose draft has not changed since last publication.

```bash
# Draft representation
curl 'http://localhost:1337/api/restaurants?status=draft&publicationFilter=unmodified' \
  -H 'Authorization: Bearer <token>'

# Published representation
curl 'http://localhost:1337/api/restaurants?publicationFilter=unmodified' \
  -H 'Authorization: Bearer <token>'
```

**中文译文:** `unmodified` 选择 draft 与最近一次 published version 内容没有变化的 documents。可以用 `status=draft` 返回 draft representation，也可以用 REST 默认 published 返回 live version。

## Find documents with a published version

**Original:** `has-published-version` selects documents that have both draft and published versions for the same locale.

```bash
curl 'http://localhost:1337/api/restaurants?status=draft&publicationFilter=has-published-version' \
  -H 'Authorization: Bearer <token>'
```

**中文译文:** `has-published-version` 按单 locale 判断：该 locale 必须同时存在 draft counterpart 与 published version。

**Original:** With REST default status, the same filter returns the currently live versions.

**中文译文:** 不传 `status` 时，由于 REST 默认 published，返回的就是这些 documents 当前 live version。

## Published in at least one locale

**Original:** `has-published-version-document` considers all locales. If one locale is published, the whole document matches.

```bash
curl 'http://localhost:1337/api/restaurants?status=draft&publicationFilter=has-published-version-document' \
  -H 'Authorization: Bearer <token>'
```

**中文译文:** `has-published-version-document` 从 document 全局判断：只要至少一个 locale 有 published version，整个 document 就匹配。配合 `status=draft` 时，可以返回这些 documents 的 draft representations，包括某些自身从未 publish 的 locales。

## Diagnostic values

**Original:** `published-without-draft` and `published-with-draft` are intended for data-integrity checks, not normal queries.

**中文译文:** `published-without-draft` 与 `published-with-draft` 主要用于 **data-integrity diagnostics**，不建议用于普通业务查询。

**Original:** In a healthy database every published document also has a draft counterpart. `published-without-draft` normally returns nothing and can reveal inconsistent legacy/manual DB data.

**中文译文:** 正常 Strapi database 中，每个 published document 都应有 draft counterpart。因此 `published-without-draft` 通常返回空；若返回数据，可能说明 legacy data 或手工 database 修改导致了不一致状态。

**Original:** `published-with-draft` should match every normally published document.

**中文译文:** `published-with-draft` 则选择正常同时具有 draft counterpart 的 published documents，在健康 database 中基本对应全部 published documents。

```bash
curl 'http://localhost:1337/api/restaurants?publicationFilter=published-without-draft' \
  -H 'Authorization: Bearer <token>'

curl 'http://localhost:1337/api/restaurants?publicationFilter=published-with-draft' \
  -H 'Authorization: Bearer <token>'
```

## Combine with other parameters

**Original:** `publicationFilter` can be combined with `filters`, `locale`, `populate`, and other REST parameters. All conditions are applied together.

**中文译文:** `publicationFilter` 可以与 `filters`、`locale`、`populate`、sorting、pagination 等其他 REST parameters 同时使用。所有条件共同作用于最终 query。
