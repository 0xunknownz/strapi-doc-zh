# 📖 对照翻译：Document Service API: Filters

> Source: `docusaurus/docs/cms/api/document-service/filters.md`  
> Upstream SHA: `561108949738965bb445ee7ef675fb3a0332b530`

**Original:** The Document Service API provides attribute operators (`$eq`, `$lt`, `$contains`, etc.) and logical operators (`$and`, `$or`, `$not`) to filter query results with support for case-sensitive and case-insensitive matching.

**中文译文:** Document Service API 提供 attribute operators（例如 `$eq`、`$lt`、`$contains`）以及 logical operators（`$and`、`$or`、`$not`），用于筛选 query results，并支持区分或不区分大小写的匹配。

**Original:** The Document Service API offers the ability to filter results.

**中文译文:** Document Service API 可以通过 `filters` object 对查询结果进行筛选。

**Original:**

| Operator | Description |
|---|---|
| `$eq` | Equal |
| `$eqi` | Equal (case-insensitive) |
| `$ne` | Not equal |
| `$nei` | Not equal (case-insensitive) |
| `$lt` | Less than |
| `$lte` | Less than or equal |
| `$gt` | Greater than |
| `$gte` | Greater than or equal |
| `$in` | Included in an array |
| `$notIn` | Not included in an array |
| `$contains` | Contains |
| `$notContains` | Does not contain |
| `$containsi` | Contains (case-insensitive) |
| `$notContainsi` | Does not contain (case-insensitive) |
| `$null` | Is null |
| `$notNull` | Is not null |
| `$between` | Is between |
| `$startsWith` | Starts with |
| `$startsWithi` | Starts with (case-insensitive) |
| `$endsWith` | Ends with |
| `$endsWithi` | Ends with (case-insensitive) |
| `$or` | OR expression |
| `$and` | AND expression |
| `$not` | NOT expression |

**中文译文:**

| Operator | 中文说明 |
|---|---|
| `$eq` | 等于 |
| `$eqi` | 等于，不区分大小写 |
| `$ne` | 不等于 |
| `$nei` | 不等于，不区分大小写 |
| `$lt` | 小于 |
| `$lte` | 小于或等于 |
| `$gt` | 大于 |
| `$gte` | 大于或等于 |
| `$in` | 值包含在数组中 |
| `$notIn` | 值不包含在数组中 |
| `$contains` | 包含 |
| `$notContains` | 不包含 |
| `$containsi` | 包含，不区分大小写 |
| `$notContainsi` | 不包含，不区分大小写 |
| `$null` | 为 null |
| `$notNull` | 不为 null |
| `$between` | 位于指定区间，包含边界 |
| `$startsWith` | 以指定值开头 |
| `$startsWithi` | 以指定值开头，不区分大小写 |
| `$endsWith` | 以指定值结尾 |
| `$endsWithi` | 以指定值结尾，不区分大小写 |
| `$or` | OR 逻辑 |
| `$and` | AND 逻辑 |
| `$not` | NOT 逻辑 |

## Attribute operators

**Original:** `$not` negates nested attribute conditions.

```js
const entries = await strapi.documents('api::article.article').findMany({
  filters: {
    title: {
      $not: {
        $contains: 'Hello World',
      },
    },
  },
});
```

**中文译文:** Attribute-level `$not` 用于否定嵌套条件。上例筛选 title **不包含** `Hello World` 的 entries。

**Original:** `$eq` checks equality. It can be omitted as shorthand.

```js
const entries = await strapi.documents('api::article.article').findMany({
  filters: {
    title: 'Hello World',
  },
});
```

**中文译文:** `$eq` 用于精确相等匹配；当只是普通相等条件时可以省略 operator，直接写 field value。

**Original:** `$eqi` and `$nei` are case-insensitive equality operators.

**中文译文:** `$eqi` / `$nei` 分别表示不区分大小写的等于 / 不等于。

**Original:** `$in` checks whether the field value is contained in an input list. Passing an array directly is shorthand for `$in`.

```js
const entries = await strapi.documents('api::article.article').findMany({
  filters: {
    title: ['Hello', 'Hola', 'Bonjour'],
  },
});
```

**中文译文:** `$in` 检查 field value 是否存在于给定列表。直接向 field 传入 array，可作为 `$in` 的 shorthand。

**Original:** `$notIn` excludes values contained in an input list.

**中文译文:** `$notIn` 用于排除列表中的值。

**Original:** `$lt`, `$lte`, `$gt`, and `$gte` compare ordered values.

**中文译文:** `$lt`、`$lte`、`$gt`、`$gte` 分别执行小于、小于等于、大于、大于等于比较。

```js
const entries = await strapi.documents('api::article.article').findMany({
  filters: {
    rating: {
      $gte: 5,
    },
  },
});
```

**Original:** `$between` includes both boundary values.

**中文译文:** `$between` 判断值是否位于两个输入值之间，并且**包含边界值**。

```js
const entries = await strapi.documents('api::article.article').findMany({
  filters: {
    rating: {
      $between: [1, 20],
    },
  },
});
```

**Original:** `$contains` and `$notContains` are case-sensitive; `$containsi` and `$notContainsi` are case-insensitive.

**中文译文:** `$contains` / `$notContains` 区分大小写；`$containsi` / `$notContainsi` 不区分大小写。

**Original:** `$startsWith` / `$endsWith` are case-sensitive. The `i` variants are case-insensitive.

**中文译文:** `$startsWith` / `$endsWith` 区分大小写；`$startsWithi` / `$endsWithi` 为不区分大小写的版本。

**Original:** `$null: true` matches null values; `$notNull: true` matches non-null values.

**中文译文:** `$null: true` 匹配 null 值；`$notNull: true` 匹配非 null 值。

## Logical operators

**Original:** `$and` requires all nested conditions to be true.

```js
const entries = await strapi.documents('api::article.article').findMany({
  filters: {
    $and: [
      { title: 'Hello World' },
      { createdAt: { $gt: '2021-11-17T14:28:25.843Z' } },
    ],
  },
});
```

**中文译文:** `$and` 要求所有 nested conditions 都成立。

**Original:** `$and` is implicit when multiple conditions are provided in the same object.

**中文译文:** 在同一个 `filters` object 中并列写多个 conditions 时，会隐式使用 `$and`，无需显式声明。

**Original:** `$or` requires one or more nested conditions to be true.

```js
const entries = await strapi.documents('api::article.article').findMany({
  filters: {
    $or: [
      { title: 'Hello World' },
      { createdAt: { $gt: '2021-11-17T14:28:25.843Z' } },
    ],
  },
});
```

**中文译文:** `$or` 要求至少一个 nested condition 成立。

**Original:** Logical `$not` negates nested conditions.

```js
const entries = await strapi.documents('api::article.article').findMany({
  filters: {
    $not: {
      title: 'Hello World',
    },
  },
});
```

**中文译文:** Logical `$not` 用于否定整个 nested condition object。

**Original:** `$not` can be both a logical operator and an attribute operator. `$and`, `$or`, and `$not` can be nested inside one another.

**中文译文:** `$not` 既可以作为 logical operator，也可以作为某个 attribute 的 operator。`$and`、`$or`、`$not` 可以继续相互嵌套，用于表达复杂筛选逻辑。
