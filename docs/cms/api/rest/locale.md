# 📖 对照翻译：REST API: `locale`

> Source: `docusaurus/docs/cms/api/rest/locale.md`  
> Upstream SHA: `6520a48d9a5f441881e9f6291860c0f43ab05ab9`

**Original:** The `locale` REST API parameter retrieves and manages documents in specific languages, defaulting to the application's default locale. Use it to fetch, create, update, and delete locale-specific versions of documents in both collection and single types.

**中文译文:** REST API 的 `locale` parameter 用于读取和管理特定语言的 document version。未指定时使用 application 的 default locale；它支持 collection type 和 single type 中 locale-specific document 的 GET、POST、PUT 与 DELETE 操作。

**Original:** Internationalization (i18n) adds locale-aware abilities to REST API.

**中文译文:** 启用 [Internationalization (i18n)](/cms/features/internationalization) 后，REST API 会获得按 locale 操作内容的能力。

**Original:** The locale must already have been added in the admin panel.

**中文译文:** 使用某个 locale 前，必须先在 admin panel 的 Internationalization settings 中添加该 locale。

**Original:** `locale` accepts a locale code. If omitted it uses the application's default locale. New Strapi projects default to `en`.

**中文译文:** `locale` 的值是 locale code。若省略，则使用 application default locale。新 Strapi 项目默认是 `en`，但可以在 admin panel 中修改 default locale。

**Original:** By default, `GET /api/restaurants` returns the same locale as `GET /api/restaurants?locale=en` when English is the default.

**中文译文:** 如果 English 是 default locale，则默认 `GET /api/restaurants` 与 `GET /api/restaurants?locale=en` 返回相同 locale 的内容。

## Supported use cases

**Original — Collection types:**

| Use case | Syntax |
|---|---|
| Get all documents in locale | `GET /api/restaurants?locale=fr` |
| Get one locale version | `GET /api/restaurants/:documentId?locale=fr` |
| Create in default locale | `POST /api/restaurants` |
| Create in specific locale | `POST /api/restaurants?locale=fr` |
| Create/update locale version | `PUT /api/restaurants/:documentId?locale=fr` |
| Delete locale version | `DELETE /api/restaurants/:documentId?locale=fr` |

**中文译文 — Collection types:**

| 用法 | Syntax |
|---|---|
| 获取指定 locale 的全部 documents | `GET /api/restaurants?locale=fr` |
| 获取某 document 的指定 locale version | `GET /api/restaurants/:documentId?locale=fr` |
| 在 default locale 创建 document | `POST /api/restaurants` |
| 在指定 locale 创建 document | `POST /api/restaurants?locale=fr` |
| 创建或更新 locale version | `PUT /api/restaurants/:documentId?locale=fr` |
| 删除 locale version | `DELETE /api/restaurants/:documentId?locale=fr` |

**Original — Single types:**

| Use case | Syntax |
|---|---|
| Get locale version | `GET /api/homepage?locale=fr` |
| Create/update locale version | `PUT /api/homepage?locale=fr` |
| Delete locale version | `DELETE /api/homepage?locale=fr` |

**中文译文 — Single types:**

| 用法 | Syntax |
|---|---|
| 获取指定 locale version | `GET /api/homepage?locale=fr` |
| 创建或更新 locale version | `PUT /api/homepage?locale=fr` |
| 删除 locale version | `DELETE /api/homepage?locale=fr` |

## `GET` all documents in a locale

**Original:**
```bash
curl 'http://localhost:1337/api/restaurants?locale=fr' \
  -H 'Authorization: Bearer <token>'
```

**中文译文:** 传入 `locale=fr` 后，只返回 French locale 中存在的 restaurant documents。Response 中每条 record 的 `locale` 为 `fr`。

## `GET` a document in a locale

**Original:** Collection type syntax: `GET /api/content-type-plural-name/document-id?locale=locale-code`.

**中文译文:** Collection type 中，把 `locale` 放在 `documentId` 后的 query string 中。

```bash
curl 'http://localhost:1337/api/restaurants/lr5wju2og49bf820kj9kz8c3?locale=fr' \
  -H 'Authorization: Bearer <token>'
```

**Original:** Single type syntax: `GET /api/content-type-singular-name?locale=locale-code`.

**中文译文:** Single type 不包含 `documentId` path segment，只需在 single type endpoint 后传入 `locale`。

```bash
curl 'http://localhost:1337/api/homepage?locale=fr' \
  -H 'Authorization: Bearer <token>'
```

## `POST` create a localized document

**Original:** To create a localized document from scratch, send POST to the collection endpoint. If no locale is provided, the default locale is used.

**中文译文:** 从零创建 localized document 时，对 collection endpoint 发送 `POST`。如果没有传 `locale`，使用 default locale。

**Original:** With Draft & Publish enabled, POST without `status` creates and publishes immediately. Use `?status=draft` to create a draft.

**中文译文:** 启用 Draft & Publish 后，REST `POST` 不带 `status` 会**创建并立即 publish**；若只想创建 draft，请传入 `?status=draft`。

### Create for default locale

```bash
curl -X POST \
  'http://localhost:1337/api/restaurants' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {
      "Name": "Oplato"
    }
  }'
```

**中文译文:** 未指定 locale 时，以上 request 在 application default locale 中创建 document。

### Create for a specific locale

```bash
curl -X POST \
  'http://localhost:1337/api/restaurants?locale=fr' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {
      "Name": "She'\''s Cake"
    }
  }'
```

**中文译文:** 添加 `?locale=fr` 后，新 document 会创建在 French locale。

## `PUT` create or update a locale version

**Original:** PUT to an existing document can create a missing locale version or update an existing locale version.

**中文译文:** 对已有 document 发送 `PUT` 时：
- 如果指定 locale 尚不存在，则创建该 locale version；
- 如果已经存在，则更新对应 locale version。

**Original:** When creating a localization for an existing localized entry, the request body can only contain localized fields.

**中文译文:** 为已有 localized entry 创建新 localization 时，request body **只能包含 localizable fields**。

**Original:** The content type must have `createLocalization` permission, otherwise the request returns 403.

**中文译文:** Content-Type 必须为当前 role 启用 `createLocalization` permission，否则 request 返回 `403 Forbidden`。

**Original:** You cannot change the locale of an existing localized entry. A `locale` field in the request body is ignored.

**中文译文:** 不能通过 update 改变已有 localized entry 的 locale。在 request body 中设置 `locale` attribute 会被忽略；locale 必须通过 query parameter 决定。

**Original:** With Draft & Publish enabled, PUT without `status` publishes changes immediately. Use `?status=draft` to update draft only.

**中文译文:** 启用 Draft & Publish 后，REST `PUT` 不带 `status` 会立即 publish 修改；若只更新 draft，应传 `?status=draft`。Single type 同样如此。

### Collection type

```bash
curl -X PUT \
  'http://localhost:1337/api/restaurants/lr5wju2og49bf820kj9kz8c3?locale=fr' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {
      "Name": "She'\''s Cake in French"
    }
  }'
```

**中文译文:** 该 request 为指定 `documentId` 创建或更新 French locale version。

### Single type

```bash
curl -X PUT \
  'http://localhost:1337/api/homepage?locale=fr' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "data": {
      "Title": "Page d'\''accueil"
    }
  }'
```

**中文译文:** 对 single type 使用相同机制，不需要 documentId。

## `DELETE` a locale version

**Original:** DELETE with a `locale` parameter removes only that locale version. On success it returns HTTP 204 and no response body.

**中文译文:** `DELETE` request 中指定 `locale` 后，只删除该 locale version。成功时返回 HTTP `204 No Content`，response body 为空。

```bash
# Collection type
curl -X DELETE \
  'http://localhost:1337/api/restaurants/abcdefghijklmno456?locale=fr' \
  -H 'Authorization: Bearer <token>'

# Single type
curl -X DELETE \
  'http://localhost:1337/api/homepage?locale=fr' \
  -H 'Authorization: Bearer <token>'
```
