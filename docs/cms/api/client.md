# 📖 对照翻译：Strapi Client

> Source: `docusaurus/docs/cms/api/client.md`  
> Upstream SHA: `6009c17f50771f13bbda7d2bab755ea3892bec0e`

**Original:** The Strapi Client is a JavaScript library that simplifies interactions with your Strapi back end for fetching, creating, updating, and deleting content through `collection()`, `single()`, and `files()` methods.

**中文译文:** Strapi Client 是一个 JavaScript library，用于简化与 Strapi back end 的交互。它通过 `collection()`、`single()` 和 `files()` 等 API 提供内容查询、创建、更新、删除以及 Media Library 操作。

**Original:** This guide covers setup, authentication, and key features.

**中文译文:** 本页介绍 Strapi Client 的安装、authentication、基础配置，以及 collection type、single type 与 files 的常用 methods。

## Getting Started

**Original:** Prerequisites: a running Strapi project and the Content API URL, e.g. `http://localhost:1337/api`.

**中文译文:** 前置条件：
- 已创建并启动 Strapi project；
- 已知该 instance 的 Content API base URL，例如 `http://localhost:1337/api`。

### Installation

```bash
# Yarn
yarn add @strapi/client

# NPM
npm install @strapi/client

# pnpm
pnpm add @strapi/client
```

**中文译文:** 使用项目当前 package manager 安装 `@strapi/client`。命令保持原样。

### Basic configuration

**Original:**
```js
import { strapi } from '@strapi/client';

const client = strapi({ baseURL: 'http://localhost:1337/api' });
```

**中文译文:** Import `strapi` factory，并通过包含 protocol 的 Content API `baseURL` 创建 client instance。JavaScript 与 TypeScript 用法相同。

**Original:** Browser UMD usage:

```html
<script src="https://cdn.jsdelivr.net/npm/@strapi/client"></script>
<script>
  const client = strapi.strapi({ baseURL: 'http://localhost:1337/api' });
</script>
```

**中文译文:** Browser 环境也可以通过 UMD script 直接加载 package。代码保持原样。

**Original:** `baseURL` must include `http` or `https`; invalid URLs throw `StrapiInitializationError`.

**中文译文:** `baseURL` 必须包含 `http://` 或 `https://` protocol。无效 URL 会在 initialization 时抛出 `StrapiInitializationError`。

### Authentication

**Original:** Configure API-token authentication through the `auth` option.

```js
const client = strapi({
  baseURL: 'http://localhost:1337/api',
  auth: 'your-api-token-here',
});
```

**中文译文:** 如果 Strapi instance 使用 API tokens，可以通过 `auth` option 配置。之后 client 会自动携带所需 authentication credentials。Token 无效或缺失时，可能抛出 `StrapiValidationError`。

## API Reference

| Property / Method | 中文说明 |
|---|---|
| `baseURL` | Strapi back end 的 Content API base URL |
| `fetch()` | 类似 native Fetch API 的通用 request method |
| `collection()` | 管理 collection-type resources |
| `single()` | 管理 single-type resources |
| `files()` / `files` | Media Library file 查询、上传、更新和删除 |

### General-purpose `fetch()`

**Original:**
```js
const result = await client.fetch('articles', { method: 'GET' });
```

**中文译文:** `client.fetch()` 暴露底层 fetch-style request。Path 始终相对于初始化时提供的 `baseURL`。

## Working with collection types

**Original:** `collection()` supports `find`, `findOne`, `create`, `update`, and `delete`.

**中文译文:** Collection type 通过 `client.collection('plural-api-id')` 访问：

| Method | 中文说明 |
|---|---|
| `find(queryParams?)` | 查询多个 documents，可带 filters / sort / pagination |
| `findOne(documentID, queryParams?)` | 按 `documentId` 查询一条 document |
| `create(data, queryParams?)` | 创建 document |
| `update(documentID, data, queryParams?)` | 更新 document |
| `delete(documentID, queryParams?)` | 删除 document |

**Original code (kept unchanged):**

```js
const articles = client.collection('articles');

const allArticles = await articles.find({
  locale: 'en',
  sort: 'title',
});

const singleArticle = await articles.findOne('article-document-id');

const newArticle = await articles.create({
  title: 'New Article',
  content: '...'
});

const updatedArticle = await articles.update(
  'article-document-id',
  { title: 'Updated Title' }
);

await articles.delete('article-id');
```

**中文译文:** 示例展示 collection type 的 list、single document、create、update、delete。Query parameters 与 REST API 保持一致。

## Working with single types

**Original:** `single()` supports `find`, `update`, and `delete`.

**中文译文:** Single type 使用 `client.single('singular-api-id')`：

| Method | 中文说明 |
|---|---|
| `find(queryParams?)` | 获取 single document |
| `update(data, queryParams?)` | 更新 single document |
| `delete(queryParams?)` | 删除 single document |

```js
const homepage = client.single('homepage');

const defaultHomepage = await homepage.find();

const spanishHomepage = await homepage.find({ locale: 'es' });

const updatedHomepage = await homepage.update(
  { title: 'Updated Homepage Title' },
  { status: 'draft' }
);

await homepage.delete();
```

**中文译文:** 示例展示读取 default locale、Spanish locale、只更新 draft，以及删除 single type 内容。

## Working with files

**Original:** The `files` manager accesses Media Library and manages file metadata/uploads.

**中文译文:** Strapi Client 的 `files` manager 封装 Media Library REST endpoints，可以直接操作 file metadata 与 upload。

| Method | 中文说明 |
|---|---|
| `find(params?)` | 查询 file metadata list |
| `findOne(fileId)` | 按 numeric file ID 查询单个 file |
| `update(fileId, fileInfo)` | 更新 file metadata |
| `upload(file, options)` | 上传 Blob 或 Buffer |
| `delete(fileId)` | 删除 file |

### `find()`

```js
const client = strapi({
  baseURL: 'http://localhost:1337/api',
  auth: 'your-api-token',
});

const allFiles = await client.files.find();

const imageFiles = await client.files.find({
  filters: {
    mime: { $contains: 'image' },
    name: { $contains: 'avatar' },
  },
  sort: ['name:asc'],
});
```

**中文译文:** `files.find()` 支持 REST-style filtering 与 sorting。上例只获取 MIME 中包含 `image`、name 中包含 `avatar` 的 files，并按 name ascending 排序。

### `findOne()`

```js
const file = await client.files.findOne(1);
console.log(file.name);
console.log(file.url);
console.log(file.mime);
```

**中文译文:** `findOne(fileId)` 使用 Media Library 的 numeric file ID 查询 metadata。

### `update()`

```js
const updatedFile = await client.files.update(1, {
  name: 'New file name',
  alternativeText: 'Descriptive alt text for accessibility',
  caption: 'A caption for the file',
});
```

**中文译文:** `update()` 接收 `fileId` 与 `fileInfo` object，可更新 name、alternative text 与 caption。

### `upload()`

**Original:** Upload supports `Blob` in browsers and Node.js, and `Buffer` in Node.js only.

**中文译文:** `upload()` 支持：
- Browser / Node.js：`Blob`；
- 仅 Node.js：`Buffer`。

**Original:** Method signatures:

```ts
async upload(file: Blob, options?: BlobUploadOptions): Promise<MediaUploadResponse>
async upload(file: Buffer, options: BufferUploadOptions): Promise<MediaUploadResponse>
```

**中文译文:** Blob upload 的 `options` 可省略，并可提供 `fileInfo`；Buffer upload 必须提供 `filename` 与 `mimetype`，也可附带 `fileInfo`。

#### Browser upload

```js
const client = strapi({ baseURL: 'http://localhost:1337/api' });

const fileInput = document.querySelector('input[type="file"]');
const file = fileInput.files[0];

const result = await client.files.upload(file, {
  fileInfo: {
    alternativeText: 'A user uploaded image',
    caption: 'Uploaded via browser',
  },
});
```

**中文译文:** Browser 中可直接将 `File` / `Blob` 传给 `files.upload()`。

#### Node.js Blob upload

```js
import { readFile } from 'fs/promises';

const client = strapi({ baseURL: 'http://localhost:1337/api' });

const fileContentBuffer = await readFile('./image.png');
const fileBlob = new Blob([fileContentBuffer], { type: 'image/png' });

const result = await client.files.upload(fileBlob, {
  fileInfo: {
    name: 'Image uploaded as Blob',
    alternativeText: 'Uploaded from Node.js Blob',
    caption: 'Example upload',
  },
});
```

#### Node.js Buffer upload

```js
import { readFile } from 'fs/promises';

const client = strapi({ baseURL: 'http://localhost:1337/api' });
const fileContentBuffer = await readFile('./image.png');

const result = await client.files.upload(fileContentBuffer, {
  filename: 'image.png',
  mimetype: 'image/png',
  fileInfo: {
    name: 'Image uploaded as Buffer',
    alternativeText: 'Uploaded from Node.js Buffer',
    caption: 'Example upload',
  },
});
```

**中文译文:** Buffer upload 必须显式提供 `filename` 与 `mimetype`。以上代码保持原样。

**Original:** Upload returns an array of file objects with fields such as `id`, `name`, `url`, `size`, and `mime`.

**中文译文:** Upload response 是 file object array，常见 fields 包括 `id`、`name`、`alternativeText`、`caption`、`mime`、`url`、`size`、`createdAt`、`updatedAt`。

### `delete()`

```js
const deletedFile = await client.files.delete(1);
console.log('Deleted file ID:', deletedFile.id);
console.log('Deleted file name:', deletedFile.name);
```

**中文译文:** `files.delete(fileId)` 删除指定 Media Library file，并返回被删除 file 的 metadata。

## Handling Common Errors

| Error | 中文说明 |
|---|---|
| `FileForbiddenError` | 当前 authenticated user / token 没有上传或管理 files 的 permission |
| `HTTPError` | Server unreachable、authentication failure 或其他 network / HTTP 问题 |
| Missing Parameters | Buffer upload 缺少 `filename` 或 `mimetype` |

**Original:** More details are available in the Strapi Client package README.

**中文译文:** 更完整的 API 与类型信息可参阅 `@strapi/client` package README 与 source code。
