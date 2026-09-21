# 📖 对照翻译：Filtering with the Query Engine API

> Source: `docusaurus/docs/cms/api/query-engine/filtering.md`  
> Upstream SHA: `e5f5a00e600356a6fe6f467787d003acb603f54a`

**Original:** The Query Engine API filters query results using the `where` parameter with logical operators (`$and`, `$or`, `$not`) and attribute operators (comparison, string matching, range) prefixed with `$`.

**中文译文:** Query Engine API 使用 `where` parameter 筛选结果。支持 logical operators（`$and`、`$or`、`$not`）以及比较、字符串匹配、区间等 attribute operators；所有 operator 都以 `$` 开头。

**Original:** Query Engine filtering is available on `findMany()`.

**中文译文:** Query Engine 的 filtering 主要通过 `findMany({ where: ... })` 使用。

## Logical operators

### `$and`

**Original:** All nested conditions must be `true`.

```js
const entries = await strapi.db.query('api::article.article').findMany({
  where: {
    $and: [
      { title: 'Hello World' },
      { createdAt: { $gt: '2021-11-17T14:28:25.843Z' } },
    ],
  },
});
```

**中文译文:** `$and` 要求全部 nested conditions 都成立。

**Original:** `$and` is implicit when multiple conditions are passed in the same object.

**中文译文:** 如果直接在同一个 `where` object 中并列多个 conditions，Query Engine 会隐式使用 `$and`。

### `$or`

**Original:** One or more nested conditions must be true.

**中文译文:** `$or` 要求至少一个 nested condition 成立。

```js
const entries = await strapi.db.query('api::article.article').findMany({
  where: {
    $or: [
      { title: 'Hello World' },
      { createdAt: { $gt: '2021-11-17T14:28:25.843Z' } },
    ],
  },
});
```

### `$not`

**Original:** Negates nested conditions. It can be used as a logical operator or an attribute operator.

**中文译文:** `$not` 用于否定 nested condition。它既可作为整个 `where` 的 logical operator，也可放在某个 attribute 内作为 attribute operator。

```js
const entries = await strapi.db.query('api::article.article').findMany({
  where: {
    $not: {
      title: 'Hello World',
    },
  },
});
```

**Original:** `$and`, `$or`, and `$not` can be nested within each other.

**中文译文:** `$and`、`$or`、`$not` 可以相互嵌套。

## Attribute operators

**Original:** Operator behavior may differ by database implementation because comparisons are handled by the database rather than Strapi.

**中文译文:** Attribute operator 的精确比较行为可能因 database implementation 而异，因为底层比较由 database 执行，而不是由 Strapi 统一模拟。

| Operator | Original meaning | 中文说明 |
|---|---|---|
| `$eq` | Equal | 等于 |
| `$eqi` | Equal, case-insensitive | 等于，不区分大小写 |
| `$ne` | Not equal | 不等于 |
| `$nei` | Not equal, case-insensitive | 不等于，不区分大小写 |
| `$in` | In input list | 在给定列表中 |
| `$notIn` | Not in input list | 不在给定列表中 |
| `$lt` | Less than | 小于 |
| `$lte` | Less than or equal | 小于或等于 |
| `$gt` | Greater than | 大于 |
| `$gte` | Greater than or equal | 大于或等于 |
| `$between` | Between, boundaries included | 在区间内，包含边界 |
| `$contains` | Contains, case-sensitive | 包含，区分大小写 |
| `$notContains` | Does not contain | 不包含，区分大小写 |
| `$containsi` | Contains, case-insensitive | 包含，不区分大小写 |
| `$notContainsi` | Does not contain, case-insensitive | 不包含，不区分大小写 |
| `$startsWith` | Starts with | 以指定值开头 |
| `$endsWith` | Ends with | 以指定值结尾 |
| `$null` | Is null | 为 null |
| `$notNull` | Is not null | 不为 null |

### Equality shorthand

**Original:** `$eq` can be omitted.

```js
const entries = await strapi.db.query('api::article.article').findMany({
  where: {
    title: 'Hello World',
  },
});
```

**中文译文:** 普通相等条件中可以省略 `$eq`，直接传入 field value。

### `$in` shorthand

**Original:** `$in` can be omitted when passing an array.

```js
const entries = await strapi.db.query('api::article.article').findMany({
  where: {
    title: ['Hello', 'Hola', 'Bonjour'],
  },
});
```

**中文译文:** 向 field 直接传入 array 时，会作为 `$in` shorthand 处理。

### Range example

```js
const entries = await strapi.db.query('api::article.article').findMany({
  where: {
    rating: {
      $between: [1, 20],
    },
  },
});
```

**中文译文:** `$between: [1, 20]` 会匹配 1 到 20 之间的值，并包含 1 和 20。

### String matching example

```js
const entries = await strapi.db.query('api::article.article').findMany({
  where: {
    title: {
      $containsi: 'hello',
    },
  },
});
```

**中文译文:** `$containsi` 表示不区分大小写的 substring matching；若需区分大小写，则使用 `$contains`。

### Null example

```js
const entries = await strapi.db.query('api::article.article').findMany({
  where: {
    title: {
      $notNull: true,
    },
  },
});
```

**中文译文:** 上例只返回 `title` 不为 null 的 entries。
