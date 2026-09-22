# 📖 对照翻译：Creating components and dynamic zones with the Entity Service API

> Source: `docusaurus/docs/cms/api/entity-service/components-dynamic-zones.md`  
> Upstream SHA: `f4bb556a0830278c6b8185976c8ec3a924ec6c05`

**Original:** Use the Entity Service API to create and update components and dynamic zones while creating or updating entries. Components are single objects while dynamic zones are lists of components with a `__component` type identifier.

**中文译文:** Entity Service API 可以在创建 / 更新 entry 时同时创建或更新 component 与 dynamic zone。Component 是单个 object；dynamic zone 则是 component list，每一项通过 `__component` 标识 component type。

**Original:** Entity Service is deprecated in Strapi 5. Use Document Service API for new code.

**中文译文:** **Entity Service API 在 Strapi 5 中已经 deprecated。新代码应优先使用 Document Service API。** 本页主要用于维护旧代码或迁移参考。

## Creation

**Original:** A component can be created inline while creating an entry.

```js
strapi.entityService.create('api::article.article', {
  data: {
    myComponent: {
      foo: 'bar',
    },
  },
});
```

**中文译文:** 在 `data` 中直接传入 component object，即可随 entry 一起创建 component。

**Original:** A dynamic zone is an array of components identified by `__component`.

```js
strapi.entityService.create('api::article.article', {
  data: {
    myDynamicZone: [
      {
        __component: 'compo.type',
        foo: 'bar',
      },
      {
        __component: 'compo.type2',
        foo: 'bar',
      },
    ],
  },
});
```

**中文译文:** Dynamic zone 通过 array 表示；每个元素必须带 `__component`，用于指定实际 component schema。

## Update

**Original:** If a component `id` is supplied, the existing component is updated; otherwise the old one is replaced by a newly created component.

**中文译文:** 更新 component 时：
- 传入已有 component `id`：更新该 component；
- 不传 `id`：旧 component 会被删除并创建一个新的 component。

```js
strapi.entityService.update('api::article.article', 1, {
  data: {
    myComponent: {
      id: 1,
      foo: 'bar',
    },
  },
});
```

**Original:** Dynamic-zone items behave the same way: existing IDs update; entries without IDs are newly created and unmatched old items are removed.

**中文译文:** Dynamic zone 中的 component items 同理：带已有 `id` 的 item 被更新；不带 `id` 的 item 会新建；未继续保留的旧 items 会被删除。
