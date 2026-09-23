# 📖 对照翻译：使用 Entity Service API 筛选数据

> Source: `docusaurus/docs/cms/api/entity-service/filter.md`  
> Upstream commit: `d3cbe0c728c53920d40e3963c0a57cca0d68dbeb`  
> Upstream blob SHA: `0ad9545ac04d3e9ef826d7e5ef512546f6e2d070`  
> [查看固定版本英文源文件](https://github.com/strapi/documentation/blob/d3cbe0c728c53920d40e3963c0a57cca0d68dbeb/docusaurus/docs/cms/api/entity-service/filter.md)

> 排版说明：MDX 的链接与图标转换为 GitHub 可读形式；正文、表格和提示逐项对照，代码块保留原样。页面元数据中的描述也在下方翻译。

> 依赖说明：下文展开了上游 `entity-service-deprecated.md` 和 `deep-filtering-blog.md` 的提示内容，不将这两个引用重复计为新增译文文件。

**Original:** Use Strapi's Entity Service API to filter your queries results.

**中文译文:** 使用 Strapi 的 Entity Service API 筛选查询结果。

<a id="filtering-with-the-entity-service-api"></a>

**Original:** Filtering with the Entity Service API

**中文译文:** 使用 Entity Service API 筛选数据

**Original:** Filter Entity Service API query results using logical operators (`$and`, `$or`, `$not`) and attribute operators (`$eq`, `$contains`, `$gt`, `$between`, etc.) with the `filters` parameter in `findMany()`.

**中文译文:** 在 `findMany()` 的 `filters` 参数中使用逻辑运算符（`$and`、`$or`、`$not`）和属性运算符（`$eq`、`$contains`、`$gt`、`$between` 等），即可筛选 Entity Service API 的查询结果。

**Original:** The Entity Service API is deprecated in Strapi v5. Please consider using the [Document Service API](/cms/api/document-service) instead.

**中文译文:** Entity Service API 在 Strapi v5 中已弃用。请考虑改用 [Document Service API](/cms/api/document-service)。

**Original:** The [Entity Service API](/cms/api/entity-service) offers the ability to filter results found with its [findMany()](/cms/api/entity-service/crud#findmany) method.

**中文译文:** [Entity Service API](/cms/api/entity-service) 支持筛选其 [`findMany()`](/cms/api/entity-service/crud#findmany) 方法查询到的结果。

**Original:** Results are filtered with the `filters` parameter that accepts [logical operators](#logical-operators) and [attribute operators](#attribute-operators). Every operator should be prefixed with `$`.

**中文译文:** 通过 `filters` 参数筛选结果。该参数接受[逻辑运算符](#logical-operators)和[属性运算符](#attribute-operators)，所有运算符都必须以 `$` 开头。

> **Deep filtering with the various APIs / 使用不同 API 进行深层筛选**

**Original:** For examples of how to deep filter with the various APIs, please refer to [this blog article](https://strapi.io/blog/deep-filtering-alpha-26).

**中文译文:** 有关使用不同 API 进行深层筛选的示例，请参阅[这篇博客文章](https://strapi.io/blog/deep-filtering-alpha-26)。

<a id="logical-operators"></a>

## Logical operators / 逻辑运算符

<a id="and"></a>

### `$and`

**Original:** All nested conditions must be `true`.

**中文译文:** 所有嵌套条件都必须为 `true`。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    $and: [
      {
        title: 'Hello World',
      },
      {
        createdAt: { $gt: '2021-11-17T14:28:25.843Z' },
      },
    ],
  },
});
```

**Original:** `$and` will be used implicitly when passing an object with nested conditions:

**中文译文:** 传入包含多个嵌套条件的对象时，会隐式使用 `$and`：

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: 'Hello World',
    createdAt: { $gt: '2021-11-17T14:28:25.843Z' },
  },
});
```

<a id="or"></a>

### `$or`

**Original:** One or many nested conditions must be `true`.

**中文译文:** 至少一个嵌套条件必须为 `true`。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    $or: [
      {
        title: 'Hello World',
      },
      {
        createdAt: { $gt: '2021-11-17T14:28:25.843Z' },
      },
    ],
  },
});
```

<a id="not"></a>

### `$not`

**Original:** Negates the nested conditions.

**中文译文:** 对嵌套条件取反。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    $not: {
      title: 'Hello World',
    },
  },
});
```

> **note / 说明**

**Original:** `$not` can be used as:

**中文译文:** `$not` 可以用作：

**Original:**

- a logical operator (e.g. in `filters: { $not: { // conditions… }}`)
- [an attribute operator](#not-1) (e.g. in `filters: { attribute-name: $not: { … } }`).

**中文译文:**

- 逻辑运算符，例如 `filters: { $not: { // conditions… }}`。
- [属性运算符](#not-1)，例如 `filters: { attribute-name: $not: { … } }`。

> **tip / 提示**

**Original:** `$and`, `$or` and `$not` operators are nestable inside of another `$and`, `$or` or `$not` operator.

**中文译文:** `$and`、`$or` 和 `$not` 可以嵌套在另一个 `$and`、`$or` 或 `$not` 运算符中。

<a id="attribute-operators"></a>

## Attribute Operators / 属性运算符

> **caution / 注意**

**Original:** Using these operators may give different results depending on the database's implementation, as the comparison is handled by the database and not by Strapi.

**中文译文:** 使用这些运算符时，结果可能因数据库的实现而异，因为比较操作由数据库执行，而不是由 Strapi 执行。

<a id="not-1"></a>

### `$not`

**Original:** Negates the nested condition(s).

**中文译文:** 对嵌套条件取反。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $not: {
        $contains: 'Hello World',
      },
    },
  },
});
```

<a id="eq"></a>

### `$eq`

**Original:** Attribute equals input value.

**中文译文:** 属性值等于输入值。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $eq: 'Hello World',
    },
  },
});
```

**Original:** `$eq` can be omitted:

**中文译文:** 可以省略 `$eq`：

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: 'Hello World',
  },
});
```

<a id="eqi"></a>

### `$eqi`

**Original:** Attribute equals input value (case-insensitive).

**中文译文:** 属性值等于输入值，不区分大小写。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $eqi: 'HELLO World',
    },
  },
});
```

<a id="ne"></a>

### `$ne`

**Original:** Attribute does not equal input value.

**中文译文:** 属性值不等于输入值。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $ne: 'ABCD',
    },
  },
});
```

<a id="nei"></a>

### `$nei`

**Original:** Attribute does not equal input value (case-insensitive).

**中文译文:** 属性值不等于输入值，不区分大小写。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $nei: 'abcd',
    },
  },
});
```

<a id="in"></a>

### `$in`

**Original:** Attribute is contained in the input list.

**中文译文:** 属性值包含在输入列表中。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $in: ['Hello', 'Hola', 'Bonjour'],
    },
  },
});
```

**Original:** `$in` can be omitted when passing an array of values:

**中文译文:** 传入值数组时，可以省略 `$in`：

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: ['Hello', 'Hola', 'Bonjour'],
  },
});
```

<a id="notin"></a>

### `$notIn`

**Original:** Attribute is not contained in the input list.

**中文译文:** 属性值不包含在输入列表中。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $notIn: ['Hello', 'Hola', 'Bonjour'],
    },
  },
});
```

<a id="lt"></a>

### `$lt`

**Original:** Attribute is less than the input value.

**中文译文:** 属性值小于输入值。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    rating: {
      $lt: 10,
    },
  },
});
```

<a id="lte"></a>

### `$lte`

**Original:** Attribute is less than or equal to the input value.

**中文译文:** 属性值小于或等于输入值。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    rating: {
      $lte: 10,
    },
  },
});
```

<a id="gt"></a>

### `$gt`

**Original:** Attribute is greater than the input value.

**中文译文:** 属性值大于输入值。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    rating: {
      $gt: 5,
    },
  },
});
```

<a id="gte"></a>

### `$gte`

**Original:** Attribute is greater than or equal to the input value.

**中文译文:** 属性值大于或等于输入值。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    rating: {
      $gte: 5,
    },
  },
});
```

<a id="between"></a>

### `$between`

**Original:** Attribute is between the 2 input values, boundaries included (e.g., `$between[1, 3]` will also return `1` and `3`).

**中文译文:** 属性值介于两个输入值之间，包含边界值。例如，`$between[1, 3]` 也会返回 `1` 和 `3`。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    rating: {
      $between: [1, 20],
    },
  },
});
```

<a id="contains"></a>

### `$contains`

**Original:** Attribute contains the input value (case-sensitive).

**中文译文:** 属性值包含输入值，区分大小写。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $contains: 'Hello',
    },
  },
});
```

<a id="notcontains"></a>

### `$notContains`

**Original:** Attribute does not contain the input value (case-sensitive).

**中文译文:** 属性值不包含输入值，区分大小写。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $notContains: 'Hello',
    },
  },
});
```

<a id="containsi"></a>

### `$containsi`

**Original:** Attribute contains the input value. `$containsi` is not case-sensitive, while [$contains](#contains) is.

**中文译文:** 属性值包含输入值。`$containsi` 不区分大小写，而 [`$contains`](#contains) 区分大小写。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $containsi: 'hello',
    },
  },
});
```

<a id="notcontainsi"></a>

### `$notContainsi`

**Original:** Attribute does not contain the input value. `$notContainsi` is not case-sensitive, while [$notContains](#notcontains) is.

**中文译文:** 属性值不包含输入值。`$notContainsi` 不区分大小写，而 [`$notContains`](#notcontains) 区分大小写。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $notContainsi: 'hello',
    },
  },
});
```

<a id="startswith"></a>

### `$startsWith`

**Original:** Attribute starts with input value.

**中文译文:** 属性值以输入值开头。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $startsWith: 'ABCD',
    },
  },
});
```

<a id="endswith"></a>

### `$endsWith`

**Original:** Attribute ends with input value.

**中文译文:** 属性值以输入值结尾。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $endsWith: 'ABCD',
    },
  },
});
```

<a id="null"></a>

### `$null`

**Original:** Attribute is `null`.

**中文译文:** 属性值为 `null`。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $null: true,
    },
  },
});
```

<a id="notnull"></a>

### `$notNull`

**Original:** Attribute is not `null`.

**中文译文:** 属性值不为 `null`。

**Original:** **Example**

**中文译文:** **示例**

```js
const entries = await strapi.entityService.findMany('api::article.article', {
  filters: {
    title: {
      $notNull: true,
    },
  },
});
```
