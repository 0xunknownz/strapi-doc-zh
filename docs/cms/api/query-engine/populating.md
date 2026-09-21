# 📖 对照翻译：Populating with the Query Engine API

> Source: `docusaurus/docs/cms/api/query-engine/populating.md`  
> Upstream SHA: `2dc1058cbd143292304b1cba2d6b116f24585834`

**Original:** The Query Engine API's `populate` parameter loads related data in queries, supporting basic population, selective attributes, filtering nested relations, and polymorphic structures via populate fragments.

**中文译文:** Query Engine API 的 `populate` parameter 用于加载 related data，支持基本 relation population、选择 attributes、筛选 nested relations，以及通过 populate fragments 处理 polymorphic structures。

**Original:** Relations and components use a unified population API.

**中文译文:** Query Engine 对 relations 和 components 使用统一的 population syntax。

**Original:** Populate all root-level relations with `populate: true`.

```js
strapi.db.query('api::article.article').findMany({
  populate: true,
});
```

**中文译文:** `populate: true` 会加载所有 root-level relations。

**Original:** Select relations by passing an array of attribute names.

```js
strapi.db.query('api::article.article').findMany({
  populate: ['componentA', 'relationA'],
});
```

**中文译文:** 传入 attribute name array 可以只 population 指定 relations / components。

**Original:** An object enables advanced conditional population.

```js
strapi.db.query('api::article.article').findMany({
  populate: {
    componentB: true,
    dynamiczoneA: true,
    relation: someLogic || true,
  },
});
```

**中文译文:** 使用 object syntax 可以为每个 relation 配置不同 population strategy，也可以由程序逻辑决定是否 population。

**Original:** Complex population supports `where`, `select`, `orderBy`, and nested `populate`.

```js
strapi.db.query('api::article.article').findMany({
  populate: {
    relationA: {
      where: {
        name: {
          $contains: 'Strapi',
        },
      },
    },

    repeatableComponent: {
      select: ['someAttributeName'],
      orderBy: ['someAttributeName'],
      populate: {
        componentRelationA: true,
      },
    },

    dynamiczoneA: true,
  },
});
```

**中文译文:** Population object 内可以继续使用：
- `where`：筛选 related entries；
- `select`：限制返回 attributes；
- `orderBy`：排序；
- nested `populate`：继续加载更深层 relation。

**Original:** For polymorphic structures such as dynamic zones and polymorphic relations, use populate fragments through `on`.

**中文译文:** 对 dynamic zone、polymorphic relation 等多态内容结构，可以使用 `on` 定义 populate fragments，对不同 component / target type 使用不同查询策略。

```js
strapi.db.query('api::article.article').findMany({
  populate: {
    dynamicZone: {
      on: {
        'components.foo': {
          select: ['title'],
          where: { title: { $contains: 'strapi' } },
        },
        'components.bar': {
          select: ['name'],
        },
      },
    },

    morphAuthor: {
      on: {
        'plugin::users-permissions.user': {
          select: ['username'],
        },
        'api::author.author': {
          select: ['name'],
        },
      },
    },
  },
});
```

**中文译文:** 上例针对不同 dynamic-zone components 与 polymorphic author types 分别定义 selection / filtering。代码保持原样。
