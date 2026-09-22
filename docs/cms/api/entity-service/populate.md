# 📖 对照翻译：Populating with the Entity Service API

> Source: `docusaurus/docs/cms/api/entity-service/populate.md`  
> Upstream SHA: `ff080b1da79bfdb9c2208fc0687bddd82e31c093`

**Original:** Entity Service `populate` retrieves relations, components, and dynamic zones; use wildcard, arrays, objects, or polymorphic fragments.

**中文译文:** Entity Service 默认不会返回 relations、components 或 dynamic zones。通过 `populate` 可使用 wildcard、attribute array、advanced object 或 polymorphic fragments 加载这些内容。

**Original:** Entity Service is deprecated in Strapi 5.

**中文译文:** Entity Service 已在 Strapi 5 deprecated，新代码应使用 Document Service API。

## Basic populating

**Original:** Populate all root-level relations with `populate: '*'`.

```js
const entries = await strapi.entityService.findMany(
  'api::article.article',
  {
    populate: '*',
  }
);
```

**中文译文:** `populate: '*'` 加载 root-level relation / component fields。

**Original:** Populate selected fields with an array.

```js
populate: ['componentA', 'relationA']
```

**中文译文:** 传入 attribute names array，可以只加载指定 relation / component。

## Advanced populating

**Original:** Object syntax supports fields, filters, sort, and nested populate.

```js
const entries = await strapi.entityService.findMany(
  'api::article.article',
  {
    populate: {
      relationA: true,
      repeatableComponent: {
        fields: ['fieldA'],
        filters: {},
        sort: 'fieldA:asc',
        populate: {
          relationB: true,
        },
      },
    },
  }
);
```

**中文译文:** Advanced populate object 可以对 nested structure 独立设置：
- `fields`
- `filters`
- `sort`
- nested `populate`

## Populate fragments

**Original:** Polymorphic content structures can use `on` fragments.

```js
populate: {
  dynamicZone: {
    on: {
      'components.foo': {
        fields: ['title'],
        filters: {
          title: {
            $contains: 'strapi',
          },
        },
      },
      'components.bar': {
        fields: ['name'],
      },
    },
  },
}
```

**中文译文:** 对 dynamic zone、polymorphic relation 等结构，`on` 可以按具体 component / target type 定义不同 populate strategy。
