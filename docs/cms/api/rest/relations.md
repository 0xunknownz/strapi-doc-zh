# 📖 对照翻译：Managing relations with API requests

> Source: `docusaurus/docs/cms/api/rest/relations.md`  
> Upstream SHA: `2e2f5bfd9958d8505805aa3075e25ca58aa69ca0`

**Original:** Use `connect`, `disconnect`, and `set` parameters in REST and GraphQL API requests to manage relations between content-types. Reorder relations using positional arguments like `before`, `after`, `start`, or `end`.

**中文译文:** 可以在 REST / GraphQL API request body 中使用 `connect`、`disconnect` 和 `set` 管理 content-types 之间的 relations；还可以通过 `before`、`after`、`start`、`end` 等 positional arguments 调整多值 relation 的顺序。

**Original:** Defining relations between content-types is connecting database entities with each other.

**中文译文:** 在 database layer 中，为 content-types 定义 relation，本质上就是把不同 entities 连接起来。

**Original:** Relations can be managed through the admin panel, REST API, or Document Service API.

**中文译文:** Relation 既可以通过 Content Manager 中的 relational fields 管理，也可以通过 REST API 或 Document Service API request 管理。

**Original:** `connect`, `disconnect`, and `set` payloads work for single-entry relations and multi relations. Multi relations expect arrays of relation IDs and return arrays.

**中文译文:** `connect`、`disconnect`、`set` 的 payload shape 同时适用于 single-entry relation 与 multi relation（one-to-many、many-to-one、many-to-many、many-way）。允许多个 links 的 relational field 需要传 array，并在 response 中返回 array。

| Parameter | Original behavior | 中文说明 | Update type |
|---|---|---|---|
| `connect` | Connects new entities; can combine with `disconnect`; supports positions | 新增 relation，不删除现有 relation；可与 `disconnect` 同时使用，也可设置 relation 顺序 | Partial |
| `disconnect` | Disconnects entities; can combine with `connect` | 删除指定 relation，保留其他 relation；可与 `connect` 同时使用 | Partial |
| `set` | Replaces all existing relations | 用给定集合完整替换当前 relations；不能与 `connect` / `disconnect` 同时使用 | Full |

**Original:** The same object shapes also work in Document Service methods. TypeScript may currently report `TS2353` for `connect`, `disconnect`, or `set`; this is a typings gap, not a runtime limitation.

**中文译文:** 本页描述的 `connect` / `disconnect` / `set` object shape 同样适用于 Document Service。当前某些 TypeScript 类型定义可能对这些字段报告 `TS2353`；这是 typings gap，并不表示 runtime 不支持。如果需要，可暂时对 relation data 做更宽泛的 type assertion。

**Original:** With i18n enabled, a locale can be passed when managing relations through Document Service.

```js
await strapi.documents('api::restaurant.restaurant').update({
  documentId: 'a1b2c3d4e5f6g7h8i9j0klm',
  locale: 'fr',
  data: {
    category: {
      connect: ['z0y2x4w6v8u1t3s5r7q9onm', 'j9k8l7m6n5o4p3q2r1s0tuv']
    }
  }
})
```

**中文译文:** 启用 i18n 时，可以在 Document Service update 中传入 `locale`，只修改对应 locale version 的 relations。未传 locale 时使用 default locale。

## `connect`

**Original:** `connect` performs a partial update and adds specified relations.

**中文译文:** `connect` 执行 partial update，只新增指定 relations，不覆盖当前已有的其他 relations。

**Original:** Shorthand and longhand syntax:

```js
connect: [
  'z0y2x4w6v8u1t3s5r7q9onm',
  'j9k8l7m6n5o4p3q2r1s0tuv'
]
```

```js
connect: [
  { documentId: 'z0y2x4w6v8u1t3s5r7q9onm' },
  { documentId: 'j9k8l7m6n5o4p3q2r1s0tuv' }
]
```

**中文译文:** Shorthand 直接使用 `documentId` array；longhand 使用 object array。需要 relation reordering 时必须使用 longhand syntax。

**Original:** `connect` can be combined with `disconnect`.

**中文译文:** 同一个 update request 中可以同时使用 `connect` 与 `disconnect`，实现 relation 的局部增删。

**Original:** `connect` is not officially supported for media attributes. Connecting upload-file IDs is an unsupported workaround that can break, especially with Draft & Publish.

**中文译文:** `connect` **不正式支持 media attributes**。虽然高级用户可能通过 upload file ID 强行连接 media entry，但 Strapi 不推荐也不支持这种方式，尤其在 Draft & Publish 下可能因 ID 不匹配导致错误。

### Shorthand request example

```http
PUT http://localhost:1337/api/restaurants/a1b2c3d4e5f6g7h8i9j0klm
```

```js
{
  data: {
    categories: {
      connect: [
        'z0y2x4w6v8u1t3s5r7q9onm',
        'j9k8l7m6n5o4p3q2r1s0tuv'
      ]
    }
  }
}
```

**中文译文:** 上例为指定 restaurant 连接两个由 `documentId` 标识的 categories，同时保留已有 categories。

### Longhand request example

```js
{
  data: {
    categories: {
      connect: [
        { documentId: 'z0y2x4w6v8u1t3s5r7q9onm' },
        { documentId: 'j9k8l7m6n5o4p3q2r1s0tuv' }
      ]
    }
  }
}
```

**中文译文:** Longhand 结果相同，但 object form 还可以加入 `position`、`locale`、`status` 等更细粒度参数。

## Relations reordering

**Original:** Positional arguments in longhand `connect` define the order of relations.

**中文译文:** Longhand `connect` 可以通过 `position` object 指定新增 relation 在 relation list 中的位置。

| Position | Original description | 中文说明 |
|---|---|---|
| `before: documentId` | Before the target relation | 放到指定 `documentId` 之前 |
| `after: documentId` | After the target relation | 放到指定 `documentId` 之后 |
| `start: true` | At the start | 放到 relation list 最前面 |
| `end: true` | At the end | 放到 relation list 最后面 |

**Original:** `position` is optional and defaults to `{ end: true }`.

**中文译文:** `position` 可省略；省略时等同于 `position: { end: true }`。

**Original:** Since `connect` is an array, operations are processed sequentially.

**中文译文:** `connect` 是 array，因此 position operations **按数组顺序依次执行**；后一项看到的是前一项已经修改后的 relation list。

**Original:** The same relation must not be connected more than once or the API returns a validation error.

**中文译文:** 同一个 relation 不应在一次 request 中重复 connect，否则 API 会返回 Validation error。

### Basic position example

```js
{
  data: {
    categories: {
      connect: [
        {
          documentId: 'ma12bc34de56fg78hi90jkl',
          position: {
            before: 'z0y2x4w6v8u1t3s5r7q9onm'
          }
        }
      ]
    }
  }
}
```

**中文译文:** 上例把新 category 插到 `z0y2x4w6v8u1t3s5r7q9onm` 对应 relation 之前。

### Combined ordering example

```js
{
  data: {
    categories: {
      connect: [
        { documentId: '6u86wkc6x3parjd4emikhmx', position: { after: 'j9k8l7m6n5o4p3q2r1s0tuv'} },
        { documentId: '3r1wkvyjwv0b9b36s7hzpxl', position: { before: 'z0y2x4w6v8u1t3s5r7q9onm' } },
        { documentId: 'rkyqa499i84197l29sbmwzl', position: { end: true } },
        { documentId: 'srkvrr77k96o44d9v6ef1vu' },
        { documentId: 'nyk7047azdgbtjqhl7btuxw', position: { start: true } }
      ]
    }
  }
}
```

**中文译文:** 该示例组合使用 `after`、`before`、`end`、默认 end 与 `start`。由于逐项执行，最终顺序取决于 array 中 operations 的执行次序。

## Edge cases: i18n / Draft & Publish

**Original:** If the source content type has i18n disabled but the target has i18n enabled, specify the target locale in longhand connect.

```js
data: {
  categories: {
    connect: [
      { documentId: 'z0y2x4w6v8u1t3s5r7q9onm', locale: 'en' },
      { documentId: 'z0y2x4w6v8u1t3s5r7q9onm', locale: 'fr' }
    ]
  }
}
```

**中文译文:** 当 relation target 启用了 i18n 时，可以用同一个 `documentId` 配合不同 `locale`，连接目标 document 的不同 locale versions。

**Original:** If the target has Draft & Publish enabled, longhand connect can target `draft` or `published`.

```js
data: {
  categories: {
    connect: [
      { documentId: 'z0y2x4w6v8u1t3s5r7q9onm', status: 'draft' },
      { documentId: 'z0y2x4w6v8u1t3s5r7q9onm', status: 'published' }
    ]
  }
}
```

**中文译文:** Relation target 启用 Draft & Publish 时，可通过 `status` 明确连接其 draft 或 published database version。

## `disconnect`

**Original:** `disconnect` performs a partial update, removing only specified relations. It supports shorthand and longhand syntax and can be combined with `connect`.

**中文译文:** `disconnect` 执行 partial update，只移除指定 relations，其他 relations 保持不变。它同样支持 shorthand / longhand，并可以与 `connect` 同时使用。

```js
{
  data: {
    categories: {
      disconnect: [
        'z0y2x4w6v8u1t3s5r7q9onm',
        'j9k8l7m6n5o4p3q2r1s0tuv'
      ]
    }
  }
}
```

```js
{
  data: {
    categories: {
      disconnect: [
        { documentId: 'z0y2x4w6v8u1t3s5r7q9onm' },
        { documentId: 'j9k8l7m6n5o4p3q2r1s0tuv' }
      ]
    }
  }
}
```

## `set`

**Original:** `set` performs a full update, replacing all existing relations with exactly the supplied set and order.

**中文译文:** `set` 执行 full update：当前 field 的全部已有 relations 都会被替换，只保留 request 中给出的关系，并采用给定顺序。

**Original:** `set` cannot be combined with `connect` or `disconnect`.

**中文译文:** `set` 不应与 `connect` / `disconnect` 同时使用。需要 partial update 时应改用 connect / disconnect。

**Original:** Shorthand and longhand syntax:

```js
set: [
  'z0y2x4w6v8u1t3s5r7q9onm',
  'j9k8l7m6n5o4p3q2r1s0tuv'
]
```

```js
set: [
  { documentId: 'z0y2x4w6v8u1t3s5r7q9onm' },
  { documentId: 'j9k8l7m6n5o4p3q2r1s0tuv' }
]
```

**中文译文:** 两种写法都会完整替换 relation list。

**Original:** Omitting the `set` wrapper and assigning an array directly is equivalent to `set`.

**中文译文:** 对 relation field 直接赋值 array（不写 `set` wrapper）也等价于 full `set` update。

```js
{
  data: {
    categories: [
      'z0y2x4w6v8u1t3s5r7q9onm',
      'j9k8l7m6n5o4p3q2r1s0tuv'
    ]
  }
}
```
