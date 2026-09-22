# 📖 对照翻译：Manipulating documents and entries with TypeScript

> Source: `docusaurus/docs/cms/typescript/documents-and-entries.md`  
> Upstream SHA: `8d58cbaefe9c59e6ad473ac34924610299600552`

**Original:** Use the `UID` and `Data` namespaces for type-safe document, content-type, and component operations.

**中文译文:** Strapi 5 提供 `UID` 与 `Data` namespaces，帮助 TypeScript project 对 document、content-type、component 做类型安全的处理，并获得 schema-aware autocomplete。

## Prerequisites

**Original:** Use Strapi v5 with TypeScript enabled and generated application types.

**中文译文:** 建议先确保：
- 项目为 Strapi 5；
- 已启用 TypeScript；
- 已运行 `ts:generate-types`，或开启 automatic type generation。

## `UID` namespace

```ts
import type { UID } from '@strapi/strapi';
```

**中文译文:**
- `UID.ContentType`：当前 application 全部 content-type UID 的 literal union；
- `UID.Component`：全部 component UID；
- `UID.Schema`：content-type 与 component 的全集；
- 还有其他更细粒度 UID types。

## `Data` namespace

```ts
import type { Data } from '@strapi/strapi';
```

**中文译文:**
- `Data.ContentType`：Strapi document object；
- `Data.Component`：component object；
- `Data.Entity`：document 或 component。

Generated schema types 决定这些 types 的最终结构；如果 schema 已变更但 types 不匹配，应重新生成 typings。

## Generic entities

### Generic document

```ts
async function save(
  name: string,
  document: Data.ContentType
) {
  await writeCSV(name, document);
}
```

**中文译文:** 不指定 UID 时，只能安全访问所有 content-types 共同拥有的 properties，例如 `id`、`documentId`、timestamps 等。业务 field 应使用 type guard 检查：

```ts
if ('my_prop' in document) {
  return document.my_prop;
}
```

### Generic component

```ts
function renderComponent(
  parent: Node,
  component: Data.Component
) {
  const properties = Object.entries(component);
  // ...
}
```

**中文译文:** Generic component 中 property names 通常只能被推断为 `string`，values 则较宽泛。

## Known entities

### Known document

```ts
function validateArticle(
  article: Data.ContentType<'api::article.article'>
) {
  const { title, category } = article;

  if (title.length < 5) {
    throw new Error('Title too short');
  }
}
```

**中文译文:** 将具体 content-type UID 作为 type parameter 后，IDE 能知道 `title`、`category` 等业务 fields 的实际类型。

### Known component

```ts
function processUsageMetrics(
  id: string,
  metrics: Data.Component<'app.metrics'>
) {
  telemetry.send(id, {
    clicks: metrics.clicks,
    views: metrics.views,
  });
}
```

## Entity subsets

**Original:** The second type parameter selects a subset of keys.

```ts
type Credentials =
  Data.ContentType<
    'api::account.account',
    'email' | 'password'
  >;
```

**中文译文:** 第二个 generic parameter `TKeys` 可把 type 缩小到指定字段集合。

## Type argument inference

**Original:** Bind the entity type to a UID generic.

```ts
function display<T extends UID.ContentType>(
  uid: T,
  document: Data.ContentType<T>
) {
  // ...
}
```

**中文译文:** 通过 generic `T extends UID.ContentType`，可以让 `document` 的实际 type 自动跟随 `uid` 推断，从而防止把 category document 传给 article UID。

**Original:** Mismatched document types produce compile-time errors.

**中文译文:** 例如：
- `display('api::article.article', article)` ✅
- `display('api::article.article', category)` ❌

这样可以在 compile time 提前发现错误。
