# 📖 对照翻译：REST API: `status`

> Source: `docusaurus/docs/cms/api/rest/status.md`  
> Upstream SHA: `0efb8bb7f76a361d54132421df63a186095b05b5`

**Original:** The REST API's `status` parameter returns either published versions (default) or drafts by passing `status=draft`. It also applies to write requests: a `POST` or `PUT` request publishes immediately unless you pass `status=draft`.

**中文译文:** REST API 的 `status` parameter 用于选择 document 的 published version（默认）或 draft version；传入 `status=draft` 即可操作 draft。该 parameter 同样适用于写请求：默认情况下 `POST` / `PUT` 会立即 publish，除非显式传入 `status=draft`。

**Original:** The REST API can work with:
- `published`: published version, default
- `draft`: draft version

**中文译文:** `status` 可使用：
- `published`：操作 published version，也是 REST API 默认值；
- `draft`：操作 draft version。

**Original:** Draft & Publish must be enabled.

**中文译文:** 使用 `status` 区分 draft / published version 前，content-type 必须启用 [Draft & Publish](/cms/features/draft-and-publish)。

**Original:** REST API defaults to `published` for every request, including `POST` and `PUT`. Document Service API defaults to `draft`.

**中文译文:** REST API 对所有 requests 都默认使用 `published`，包括 `POST` 与 `PUT`。这与 Document Service API 不同，后者默认使用 `draft`。

**Original:** To select documents based on the relationship between draft and published versions, use `publicationFilter`.

**中文译文:** 如果需要按 draft / published 之间的关系筛选 documents，例如 never-published、modified 等，请使用 [`publicationFilter`](/cms/api/rest/publication-filter)。

## Read draft or published versions

**Original:** Add `status` to a `GET` request to choose the returned version. In returned draft data, `publishedAt` is `null`, even if a published version exists. Omitting `status` is equivalent to `status=published`.

**中文译文:** 在 `GET` request 中添加 `status` 可以选择返回哪个 version。返回 draft 时，response 中的 `publishedAt` 为 `null`，即使该 document 已经存在 published version。省略 `status` 等价于传入 `status=published`。

**Original:**

`GET /api/restaurants?status=draft`

```bash
curl 'http://localhost:1337/api/restaurants?status=draft' \
  -H 'Authorization: Bearer <token>'
```

```js
const qs = require('qs');
const query = qs.stringify({
  status: 'draft',
}, {
  encodeValuesOnly: true,
});

await request(`/api/restaurants?${query}`);
```

**中文译文:** 上例返回 restaurants 的 draft versions。Query 与代码保持原样。

## Create or update as draft or published

**Original:**

| Request | Result |
|---|---|
| `POST /api/:pluralApiId?status=draft` | Creates a draft |
| `POST /api/:pluralApiId` | Creates and publishes immediately |
| `PUT /api/:pluralApiId/:documentId?status=draft` | Updates draft without publishing |
| `PUT /api/:pluralApiId/:documentId` | Updates draft and publishes |
| `PUT ...` with empty `data` | Publishes draft without changing content |

**中文译文:**

| Request | 结果 |
|---|---|
| `POST /api/:pluralApiId?status=draft` | 创建 draft document |
| `POST /api/:pluralApiId` | 创建并立即 publish |
| `PUT /api/:pluralApiId/:documentId?status=draft` | 更新 draft，但不 publish 修改 |
| `PUT /api/:pluralApiId/:documentId` | 更新 draft 并 publish |
| 使用空 `data` 的 `PUT` | 不修改内容，直接 publish 当前 draft |

**Original:** The same behavior applies to single types through `PUT /api/:singularApiId`.

**中文译文:** Single type 同样支持该机制，可在 `PUT /api/:singularApiId` 上使用 `status`。

**Original:** With Draft & Publish enabled, POST or PUT without a status parameter publishes immediately. Pass `status=draft` explicitly to save without publishing.

**中文译文:** 启用 Draft & Publish 后，REST API 的 `POST` / `PUT` 如果不传 `status`，会直接 publish。若只想保存 draft，必须显式传入 `status=draft`。

**Original:** Published documents always keep a draft counterpart. Writing with `status=published` first writes the draft, then publishes it, so both versions contain the same data.

**中文译文:** Published document 始终保留一个 draft counterpart。使用 `status=published` 创建或更新时，Strapi 会先写入 draft，再 publish，因此两个 versions 初始包含相同 data。

### Create a draft

**Original:**

```bash
curl -X POST \
  'http://localhost:1337/api/restaurants?status=draft' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {
      "Name": "Biscotte Restaurant"
    }
  }'
```

**中文译文:** 通过 `POST /api/restaurants?status=draft` 创建 document 时，document 会停留在 draft；response 中 `publishedAt` 为 `null`。

### Create and publish immediately

**Original:** Omitting `status`, or passing `status=published`, creates and publishes in a single request.

**中文译文:** 省略 `status`，或显式传入 `status=published`，会在一次 request 中创建并 publish document。此时 response 中 `publishedAt` 为 timestamp。

```bash
curl -X POST \
  'http://localhost:1337/api/restaurants' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {
      "Name": "Biscotte Restaurant"
    }
  }'
```

### Update a draft without publishing it

**Original:** Pass `status=draft` to `PUT` to modify only the draft and leave the published version unchanged.

**中文译文:** 对 `PUT` request 传入 `status=draft`，只更新 draft version，不影响 published version。

```bash
curl -X PUT \
  'http://localhost:1337/api/restaurants/jae8klabhuucbkgfe2xxc5dj?status=draft' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {
      "Name": "Biscotte Restaurant (closed)"
    }
  }'
```

### Publish an existing draft

**Original:** Send a `PUT` without `status`, or with `status=published`, to publish an existing draft.

**中文译文:** 要 publish 已存在的 draft，可发送不带 `status` 的 `PUT`，或显式使用 `status=published`。

```bash
curl -X PUT \
  'http://localhost:1337/api/restaurants/jae8klabhuucbkgfe2xxc5dj' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {
      "Name": "Biscotte Restaurant (closed)"
    }
  }'
```

**Original:** PUT requires a `data` object, so this request updates and publishes in one operation.

**中文译文:** `PUT` request 必须包含 `data` object，因此上例会在同一操作中更新并 publish。

### Publish a draft without changing content

**Original:** Send an empty `data` object to publish the draft as-is.

**中文译文:** 如果只想按当前内容原样 publish draft，可传入空的 `data` object：

```bash
curl -X PUT \
  'http://localhost:1337/api/restaurants/jae8klabhuucbkgfe2xxc5dj' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {}
  }'
```

**Original:** Omitting the `data` key entirely returns a `400` error.

**中文译文:** 不能完全省略 `data` key；空 body 会返回 `400`。应发送 `"data": {}`。
