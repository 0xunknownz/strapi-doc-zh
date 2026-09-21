# 📖 对照翻译：Document Service API: Using the `locale` parameter

> Source: `docusaurus/docs/cms/api/document-service/locale.md`  
> Upstream SHA: `f5c816437240f7e6fc38ab396239e74bb88f36fa`

**Original:** The `locale` parameter in the Document Service API lets you query, create, update, delete, publish, and unpublish documents for specific language versions using methods like `findOne()`, `findMany()`, `update()`, and `delete()`.

**中文译文:** Document Service API 的 `locale` parameter 可以针对特定语言版本执行 query、create、update、delete、publish 与 unpublish，适用于 `findOne()`、`findMany()`、`update()`、`delete()` 等 methods。

**Original:** By default the Document Service API returns the application's default locale version, which is `en` unless another default locale is configured.

**中文译文:** 默认情况下，Document Service API 返回 application 的 default locale version；如果没有修改 i18n 默认设置，该 locale 为 `en`。详情参阅 [Internationalization](/cms/features/internationalization)。

## Get a locale version with `findOne()`

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').findOne({
  documentId: 'a1b2c3d4e5f6g7h8i9j0klm',
  locale: 'fr',
});
```

**中文译文:** 向 `findOne()` 传入 `locale: 'fr'`，即可获取该 document 的 French locale version。若没有传 `status`，默认返回 draft。

## Get a locale version with `findFirst()`

**Original:**
```js
const document = await strapi.documents('api::article.article').findFirst({
  locale: 'fr',
});
```

**中文译文:** `findFirst()` 只返回具有 French locale 的第一条匹配 document；默认 status 同样为 draft。

## Get locale versions with `findMany()`

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').findMany({ locale: 'fr' });
```

**中文译文:** `findMany({ locale: 'fr' })` 只返回存在 French locale version 的 documents。若没有指定 `status`，默认返回这些 documents 的 draft versions。

**Original:** If Documents A, C, and D have `fr` locales while B does not, `findMany({ locale: 'fr' })` returns A, C, and D only.

**中文译文:** 如果 A、C、D 存在 `fr` locale，而 B 没有，则该 query 只返回 A、C、D。

## Create a document for a locale

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').create({
  locale: 'es',
  data: { name: 'Restaurante B' }
})
```

**中文译文:** 在 `create()` 中传入 `locale: 'es'`，会创建 Spanish locale version。如果省略 `locale`，则在 default locale 中创建 draft。

## Update a locale version

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').update({
  documentId: 'a1b2c3d4e5f6g7h8i9j0klm',
  locale: 'es',
  data: { name: 'Nuevo nombre del restaurante' },
});
```

**中文译文:** `update()` 中传入 locale 后，只更新该 document 指定 locale version，不影响其他 locales。

## Delete locale versions

**Original:** Use `locale` with `delete()` to delete only selected locale versions. Unless a status is specified, both draft and published versions are deleted.

**中文译文:** 在 `delete()` 中传入 `locale` 可以只删除特定 locale version。如果没有额外指定 `status`，该 locale 的 draft 与 published versions 都会被删除。

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').delete({
  documentId: 'a1b2c3d4e5f6g7h8i9j0klm',
  locale: 'es',
});
```

**中文译文:** 上例只删除 Spanish locale。

**Original:** Use `locale: '*'` to delete all locale versions.

**中文译文:** 使用 wildcard `locale: '*'` 可以删除 document 的全部 locale versions。

## Publish locale versions

**Original:**
```js
await strapi.documents('api::restaurant.restaurant').publish({
  documentId: 'a1b2c3d4e5f6g7h8i9j0klm',
  locale: 'fr',
});
```

**中文译文:** `publish()` 中指定 `locale: 'fr'`，只 publish French locale version。

**Original:** Use `locale: '*'` to publish all locales.

**中文译文:** 使用 `locale: '*'` 会 publish document 当前存在的全部 locale versions。

## Unpublish locale versions

**Original:**
```js
await strapi
  .documents('api::restaurant.restaurant')
  .unpublish({ documentId: 'a1b2c3d4e5f6g7h8i9j0klm', locale: 'fr' });
```

**中文译文:** `unpublish()` 同样支持 locale。上例只 unpublish French locale version。

**Original:** Use `locale: '*'` to unpublish all locale versions.

**中文译文:** 使用 `locale: '*'` 可以一次 unpublish 全部 locale versions。

**Original:** `unpublish()` can also use `fields` to select returned fields.

**中文译文:** `unpublish()` 可以与 `fields` 组合，只返回指定 fields。

## Discard drafts for locale versions

**Original:**
```js
await strapi
  .documents('api::restaurant.restaurant')
  .discardDraft({ documentId: 'a1b2c3d4e5f6g7h8i9j0klm', locale: 'fr' });
```

**中文译文:** `discardDraft()` 中指定 locale，可以只 discard 某个 locale 的 draft data。

**Original:** Use `locale: '*'` to discard drafts for all locale versions.

**中文译文:** 使用 `locale: '*'` 可以对 document 的所有 locales 执行 discardDraft。

## Count documents for a locale

**Original:**
```js
strapi.documents('api::restaurant.restaurant').count({ locale: 'fr' });
```

**中文译文:** `count()` 同样接受 `locale`。如果没有传 `status`，默认统计 draft documents；由于 published document 也保留 draft counterpart，因此这相当于统计该 locale 可用 documents 的总数。
