# 📖 对照翻译：CRUD operations with the Entity Service API

> Source: `docusaurus/docs/cms/api/entity-service/crud.md`  
> Upstream SHA: `66b830d76d8d4c6b27eee40d9169ddbee33a88cc`

**Original:** The Entity Service API performs CRUD operations through `findOne()`, `findMany()`, `create()`, `update()`, and `delete()`, with filtering, pagination, relations, and localization.

**中文译文:** Entity Service API 通过 `findOne()`、`findMany()`、`create()`、`update()`、`delete()` 执行 CRUD，并支持 filtering、pagination、relations 与 localization。

**Original:** Entity Service is deprecated in Strapi 5.

**中文译文:** **Entity Service API 在 Strapi 5 中已 deprecated。新代码应迁移到 Document Service API。**

## UID format

**Original:** `uid` uses `[category]::[content-type]`, where category is `admin`, `plugin`, or `api`.

**中文译文:** Entity Service 的第一个参数是 content-type `uid`，格式为：

`[category]::[content-type]`

常见示例：
- Admin user：`admin::user`
- Upload file：`plugin::upload.file`
- 自定义 Article：`api::article.article`

**Original:** Run `strapi content-types:list` to list all UIDs.

**中文译文:** 可运行 `strapi content-types:list` 查看当前 instance 中全部 content-type UIDs。

## `findOne()`

**Original:** Finds one entry by numeric ID.

```js
const entry = await strapi.entityService.findOne(
  'api::article.article',
  1,
  {
    fields: ['title', 'description'],
    populate: { category: true },
  }
);
```

**中文译文:** `findOne()` 使用旧式 numeric `id`，并支持 `fields`、`populate` 与可选 `locale`。

## `findMany()`

**Original:** `findMany()` supports fields, filters, start/limit, sort, populate, publication state, and locale.

**中文译文:** `findMany()` 常用 parameters：

| Parameter | 中文说明 |
|---|---|
| `fields` | 返回哪些 attributes |
| `filters` | Filters |
| `start` / `limit` | Offset pagination |
| `sort` | 排序 |
| `populate` | Relations / components / dynamic zones |
| `publicationState` | `live` 或 `preview` |
| `locale` | i18n locale |

```js
const entries = await strapi.entityService.findMany(
  'api::article.article',
  {
    fields: ['title', 'description'],
    filters: { title: 'Hello World' },
    sort: { createdAt: 'DESC' },
    populate: { category: true },
  }
);
```

**Original:** To get draft-only entries, use `publicationState: 'preview'` and filter `publishedAt` as null.

**中文译文:** 旧 Entity Service 中没有 Strapi 5 的 `status` parameter。只查询 draft 时常用：

```js
{
  publicationState: 'preview',
  filters: {
    publishedAt: {
      $null: true,
    },
  },
}
```

## `create()`

**Original:** Creates one entry and returns it.

```js
const entry = await strapi.entityService.create(
  'api::article.article',
  {
    data: {
      title: 'My Article',
    },
  }
);
```

**中文译文:** `create()` 接收 `data`，并可同时使用 `fields`、`populate` 与 `locale`。

## Relations

**Original:** Relations can be managed in `data` with REST-style `connect`, `disconnect`, and `set`.

**中文译文:** 在 `data` object 中，relation 可使用与 REST API 相同的：
- `connect`
- `disconnect`
- `set`

具体语法参阅 [REST relations](/cms/api/rest/relations)。

## `update()`

**Original:** `update()` is partial: fields omitted from `data` are preserved.

**中文译文:** `update()` 是 partial update；没有出现在 `data` 中的现有 fields 不会被覆盖。

```js
const entry = await strapi.entityService.update(
  'api::article.article',
  1,
  {
    data: {
      title: 'xxx',
    },
  }
);
```

## `delete()`

**Original:** Deletes one entry and returns it.

```js
const entry = await strapi.entityService.delete(
  'api::article.article',
  1
);
```

**中文译文:** `delete()` 同样使用 numeric `id`；可通过 `locale` 删除指定 localization。
