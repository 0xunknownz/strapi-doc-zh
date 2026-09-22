# 📖 对照翻译：Admin Panel API — Fetch client

> Source: `docusaurus/docs/cms/plugins-development/admin-fetch-client.md`  
> Upstream SHA: `ecba7d6e3b40bdea9adc46603c47e31f4e132dc2`

**Original:** Use `useFetchClient` inside React components and `getFetchClient` elsewhere to make authenticated HTTP requests from the admin panel.

**中文译文:** Admin panel plugin 不应直接使用 raw `fetch` / `axios` 管理 authentication。Strapi 提供内置 fetch client：
- React component 内使用 `useFetchClient`；
- 非 React code 使用 `getFetchClient`。

两者都会自动附带当前 admin user authentication token。

## Methods

**Original:** Both clients expose `get`, `post`, `put`, and `del`.

**中文译文:** 两个 client 都提供：
- `get`
- `post`
- `put`
- `del`（因为 `delete` 是 JavaScript keyword）

## Inside React

```js
import { useFetchClient } from '@strapi/strapi/admin';

const MyComponent = () => {
  const { get } = useFetchClient();

  const fetchData = async () => {
    const { data } =
      await get('/my-plugin/my-endpoint');
  };
};
```

**Original:** Requests are automatically cancelled when the component unmounts.

**中文译文:** `useFetchClient` 会自动提供与 component lifecycle 绑定的 `AbortSignal`，unmount 时取消 pending request。

## Outside React

```js
import { getFetchClient } from '@strapi/strapi/admin';

const { get, del } = getFetchClient();

export const fetchItems = async () => {
  const { data } =
    await get('/my-plugin/items');

  return data;
};

export const deleteItem = async (id) => {
  await del(`/my-plugin/items/${id}`);
};
```

## Send data

```js
const { post, put } = getFetchClient();

await post('/my-plugin/items', payload);
await put(`/my-plugin/items/${id}`, payload);
```

**Original:** FormData requests automatically remove the Content-Type header so the browser can set the multipart boundary.

**中文译文:** 发送 `FormData` 时，client 会自动移除手动 `Content-Type`，让 browser 设置正确 multipart boundary。

## Request options

| Option | 中文说明 |
|---|---|
| `params` | 自动 serialize 为 query string |
| `headers` | 额外 headers，与默认值 merge |
| `signal` | AbortSignal |
| `validateStatus` | 自定义哪些 HTTP status 算 error |
| `responseType` | `json` / `blob` / `text` / `arrayBuffer`，仅 GET |

## Query params

```js
const { data } = await get(
  '/content-manager/collection-types/api::article.article',
  {
    params: {
      page: 1,
      pageSize: 10,
      sort: 'title:asc',
    },
  }
);
```

## Non-JSON responses

```js
const { data: blob, status, headers } =
  await get(url, {
    responseType: 'blob',
  });
```

**中文译文:** `blob`、`text`、`arrayBuffer` response 也会返回 `status` 与 `headers`，适合 file download、CSV export 等。

## Error handling

```js
import {
  useFetchClient,
  isFetchError,
} from '@strapi/strapi/admin';

try {
  const { data } = await get('/my-plugin/my-endpoint');
} catch (error) {
  if (isFetchError(error)) {
    console.error(
      error.status,
      error.message
    );
  } else {
    throw error;
  }
}
```

**Original:** On HTTP 401, the client automatically refreshes the auth token and retries once, except for authentication endpoints.

**中文译文:** 普通 request 返回 `401` 时，fetch client 会自动 refresh authentication token 并 retry；authentication endpoints 本身不会走自动 retry。
