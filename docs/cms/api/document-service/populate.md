# 📖 对照翻译：Document Service API: Populating fields

> Source: `docusaurus/docs/cms/api/document-service/populate.md`  
> Upstream SHA: `7694080d186b03ab6783e174fc276518cb684eb3`

**Original:** Use the `populate` parameter with the Document Service API to explicitly load relations, media fields, components, and dynamic zones at one or multiple levels deep, and within `create()`, `update()`, `publish()`, and `delete()` operations.

**中文译文:** Document Service API 默认不会加载 relations、media fields、components 或 dynamic zones。使用 `populate` parameter 可以显式加载这些结构，支持一层或多层嵌套，并且同样可以用于 `create()`、`update()`、`publish()`、`delete()` 等操作的返回结果。

**Original:** You can also use `fields` to return only specific scalar fields.

**中文译文:** 如果需要进一步减少 response，可以把 `populate` 与 `fields` 组合使用，只返回需要的 scalar fields。

**Original:** If Users & Permissions is enabled, the `find` permission must be enabled for populated content-types.

**中文译文:** 如果启用了 Users & Permissions，被 populate 的 content-type 必须对当前 role 开放 `find` permission；无权访问的 content-type 不会被 population。

## Relations and media fields

**Original:** `populate` supports all relation types, including one-to-many, many-to-one, many-to-many, and polymorphic relations.

**中文译文:** `populate` 支持全部 relation types，包括 one-to-many、many-to-one、many-to-many，以及 polymorphic relations（如 morphToOne / morphToMany）。

### Populate 1 level for all relations

**Original:**
```js
const documents = await strapi.documents("api::article.article").findMany({
  populate: "*",
});
```

**中文译文:** 使用 `populate: "*"` 可以把所有可 population 的关系结构加载 1 层。Production 中不建议无节制使用 wildcard，应优先显式选择所需 relation。

### Populate 1 level for specific relations

**Original:**
```js
const documents = await strapi.documents("api::article.article").findMany({
  populate: ["headerImage"],
});
```

**中文译文:** 使用 array 可以只 populate 指定 relations。上例只加载 `headerImage`。

### Populate several levels deep

**Original:**
```js
const documents = await strapi.documents("api::article.article").findMany({
  populate: {
    categories: {
      populate: ["articles"],
    },
  },
});
```

**中文译文:** Nested `populate` object 可以继续向下加载多层 relation。上例先加载 `categories`，再加载每个 category 的 `articles`。

### Sort populated relations

**Original:**
```js
const documents = await strapi.documents("api::article.article").findMany({
  populate: {
    categories: {
      sort: 'name:asc',
    },
  },
});
```

**中文译文:** 可以在 `populate` object 内使用 `sort` 对 related entries 排序。对 many-to-many 等 join-table relations，显式 `sort` 会覆盖默认 connect order。

**Original:** Omit `sort` to preserve the default connect order.

**中文译文:** 如果希望保持 entries 建立关联时的 connect order，请不要在 population 中设置 `sort`。

## Components & Dynamic Zones

**Original:** Empty populated `morphMany` relations return `[]` instead of `null`.

**中文译文:** 被 populate 后，如果 `morphMany` relation 为空（包括 `type: 'media', multiple: true` 等），返回值为 `[]`，而不是 `null`。

**Original:** Components are populated the same way as relations.

```js
const documents = await strapi.documents("api::article.article").findMany({
  populate: ["testComp"],
});
```

**中文译文:** Component 的 population 语法与普通 relation 一致。上例加载 `testComp` component。

**Original:** Standard populate on a dynamic zone retrieves only first-level non-relational scalar fields. It does not automatically fetch nested relations, media, or nested components.

**中文译文:** Dynamic zone 的结构更动态。普通 `populate: '*'` 或 `populate: ['testDZ']` 只会返回 dynamic zone 中各 component 的第一层 non-relational scalar fields，不会自动加载 nested relations、media fields 或 nested components。

**Original:** To populate component-specific nested content in a dynamic zone, use the `on` property (fragment population syntax).

**中文译文:** 如果需要针对 dynamic zone 内不同 component 加载各自 nested relation / media / component，必须使用 `on` property，也就是 fragment population syntax。

```js
const documents = await strapi.documents("api::article.article").findMany({
  populate: {
    testDZ: {
      on: {
        "test.test-compo": {
          fields: ["testString"],
          populate: ["testNestedCompo"],
        },
      },
    },
  },
});
```

**中文译文:** 上例针对 `test.test-compo` component，只返回 `testString`，并额外 populate `testNestedCompo`。

## Populating with `create()`

**Original:**
```js
strapi.documents("api::article.article").create({
  data: {
    title: "Test Article",
    slug: "test-article",
    body: "Test 1",
    headerImage: 2,
  },
  populate: ["headerImage"],
});
```

**中文译文:** 在 `create()` 中使用 `populate`，可以让创建完成后的 response 直接包含指定 relation，例如 `headerImage`。

## Populating with `update()`

**Original:**
```js
strapi.documents("api::article.article").update({
  documentId: "cjld2cjxh0000qzrmn831i7rn",
  data: {
    title: "Test Article Update",
  },
  populate: ["headerImage"],
});
```

**中文译文:** `update()` 同样支持 population；它不会改变 update 的写入逻辑，只控制返回结果中加载哪些关系结构。

## Populating with `publish()`

**Original:**
```js
strapi.documents("api::article.article").publish({
  documentId: "cjld2cjxh0000qzrmn831i7rn",
  populate: ["headerImage"],
});
```

**中文译文:** `publish()` 可以在 returned published versions 中 populate 指定 relation。相同机制也适用于 `unpublish()` 与 `discardDraft()`。

## Populating with `delete()`

**Original:**
```js
strapi.documents("api::article.article").delete({
  documentId: "cjld2cjxh0000qzrmn831i7rn",
  populate: ["headerImage"],
});
```

**中文译文:** `delete()` 返回被删除 entries 时，也可以通过 `populate` 让 returned entries 包含指定 relation。
