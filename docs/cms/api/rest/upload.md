# 📖 对照翻译：REST API: Upload files

> Source: `docusaurus/docs/cms/api/rest/upload.md`  
> Upstream SHA: `a3bb0ce5ea97549572b3d4bb4a35719800a083ca`

**Original:** The `/api/upload` REST API endpoints enable you to upload files to the Media Library, retrieve paginated file lists, update file metadata, and delete files from your Strapi application.

**中文译文:** `/api/upload` REST API endpoints 可以向 Media Library 上传文件、获取文件列表或分页列表、更新 file metadata，以及从 Strapi application 删除文件。

**Original:** The Media Library is powered by the `upload` package. Files can be managed from the admin panel or through REST API.

**中文译文:** Media Library 在 Strapi back-end 中由 `upload` package 提供能力。既可以直接在 admin panel 中管理文件，也可以通过 REST API 操作。

**Original:**

| Method | Path | Description |
|---|---|---|
| GET | `/api/upload/files` | Get all files |
| GET | `/api/upload/files/page` | Get paginated files |
| GET | `/api/upload/files/:id` | Get one file |
| POST | `/api/upload` | Upload files |
| POST | `/api/upload?id=x` | Update `fileInfo` |
| DELETE | `/api/upload/files/:id` | Delete a file |

**中文译文:**

| Method | Path | 说明 |
|---|---|---|
| GET | `/api/upload/files` | 获取全部 files |
| GET | `/api/upload/files/page` | 获取分页 files |
| GET | `/api/upload/files/:id` | 获取指定 file |
| POST | `/api/upload` | 上传 files |
| POST | `/api/upload?id=x` | 更新 `fileInfo` |
| DELETE | `/api/upload/files/:id` | 删除 file |

**Original:** Media Library folders are admin-panel-only and are not part of Content API. Files uploaded through REST are placed in the automatically created "API Uploads" folder.

**中文译文:** Media Library 的 folders 仅属于 admin panel 功能，不属于 Content API。通过 REST API 上传的 files 会放入自动创建的 **API Uploads** folder。

**Original:** GraphQL API does not support uploading media files. Use REST API or Media Library. Some GraphQL mutations can still update or delete uploaded media.

**中文译文:** GraphQL API 不支持上传 media files。上传操作应使用 REST API 或 admin panel 的 Media Library；不过 GraphQL 仍提供部分用于更新或删除已上传 media 的 mutations。

## Get a list of files

**Original:** `/api/upload/files` returns every file as a flat array. `/api/upload/files/page` returns a standard paginated response. Prefer the paginated endpoint for non-trivial libraries.

**中文译文:** `/api/upload/files` 会把所有 files 作为 flat array 一次返回；`/api/upload/files/page` 则使用标准 pagination response。只要 Media Library 数据量不是非常小，就优先使用分页 endpoint。

### Get all files

**Original:** `GET /api/upload/files` ignores pagination parameters and always returns all files.

**中文译文:** `GET /api/upload/files` 会忽略 pagination parameters，始终返回所有 files；大型 Media Library 中 response 可能非常大。

### Get a paginated list of files

**Original:** `GET /api/upload/files/page` supports standard REST parameters.

**中文译文:** `GET /api/upload/files/page` 支持标准 REST collection parameters：

| Parameter | 中文说明 |
|---|---|
| `pagination[page]` | 1-based page number，默认 1 |
| `pagination[pageSize]` | 每页 files 数量，默认来自 `api.rest.defaultLimit`（默认 25） |
| `pagination[start]` | Offset pagination：跳过 files 数量 |
| `pagination[limit]` | Offset pagination：最多返回 files 数量 |
| `pagination[withCount]` | 是否执行 count query，并返回 `total` / `pageCount` |
| `filters` | 筛选 files |
| `sort` | 排序 |
| `fields` | 选择返回 fields |
| `populate` | Populate relations |

**Original:** Pagination uses nested syntax such as `pagination[page]=2&pagination[pageSize]=10`. Page and offset pagination are mutually exclusive.

**中文译文:** Pagination 必须使用 nested syntax，例如 `pagination[page]=2&pagination[pageSize]=10`，而不是 flat `page=2&pageSize=10`。Page pagination 与 offset pagination 不能混用，否则返回 `400`。

**Original:** Example:

`GET /api/upload/files/page?pagination[page]=2&pagination[pageSize]=10`

**中文译文:** 上例返回第 2 页，每页 10 个 files；response 中包含标准 `meta.pagination`。

**Original:** Offset example:

`GET /api/upload/files/page?pagination[start]=20&pagination[limit]=5&pagination[withCount]=false&filters[mime][$startsWith]=image/`

**中文译文:** 上例跳过前 20 个 files，最多返回 5 个 MIME 以 `image/` 开头的 files，并关闭 count query。此时 `meta.pagination` 只返回 `start` 与 `limit`，不含 `total`、`pageCount`。

## Upload files

**Original:** Upload one or more files. `files` is the file parameter; values can be Buffer or Stream.

**中文译文:** `POST /api/upload` 可以上传一个或多个 files。`files` 是必需参数，值可以是 Buffer 或 Stream。

**Original:** With a private AWS S3 bucket, returned URLs are automatically signed when `ACL` is `"private"`. Signed URLs include `X-Amz-Signature` and `isUrlSigned: true`, and expire according to `signedUrlExpires` (default 15 minutes).

**中文译文:** 使用 private AWS S3 bucket 且 `ACL` 设置为 `"private"` 时，upload endpoints 返回的 file URL 会自动签名。Signed URL 包含 `X-Amz-Signature` query parameter，并在 response 中标记 `isUrlSigned: true`；过期时间由 `signedUrlExpires` 控制，默认 15 分钟。

**Original:** When uploading an image, include `fileInfo` to set file name, alt text, and caption.

**中文译文:** 上传 image 时，可以同时提供 `fileInfo` object，设置 file name、alternative text 和 caption。

**Original code (kept unchanged):**

```html
<form>
  <input type="file" name="files" />
  <input
    type="hidden"
    name="fileInfo"
    value='{"name":"homepage-hero","alternativeText":"Person smiling while holding laptop","caption":"Hero image used on the homepage"}'
  />
  <input type="submit" value="Submit" />
</form>

<script type="text/javascript">
  const form = document.querySelector('form');

  form.addEventListener('submit', async (e) => {
    e.preventDefault();

    await fetch('/api/upload', {
      method: 'post',
      body: new FormData(e.target)
    });
  });
</script>
```

**中文译文:** Browser 示例保持原样。Upload request body 必须使用 `FormData`。

**Original code (kept unchanged):**

```js
import { FormData } from 'formdata-node';
import fetch, { blobFrom } from 'node-fetch';

const file = await blobFrom('./1.png', 'image/png');
const form = new FormData();

form.append('files', file, "1.png");
form.append(
  'fileInfo',
  JSON.stringify({
    name: 'Homepage hero',
    alternativeText: 'Person smiling while holding laptop',
    caption: 'Hero image used on the homepage',
  })
);

const response = await fetch('http://localhost:1337/api/upload', {
  method: 'post',
  body: form,
});
```

**中文译文:** Node.js 示例同样通过 `FormData` 提交 files 与可选 `fileInfo`，代码保持原样。

## Upload entry files

**Original:** Files can be uploaded and linked directly to an entry.

**中文译文:** Upload 时也可以直接把 file 关联到某个具体 entry。

| Parameter | 中文说明 |
|---|---|
| `files` | 要上传的 file(s)，Buffer 或 Stream |
| `path` | 可选；上传 folder，仅 `strapi-provider-upload-aws-s3` 支持 |
| `refId` | 要关联 entry 的 ID |
| `ref` | Model UID，例如 `api::restaurant.restaurant` |
| `source` | 可选；model 所在 plugin |
| `field` | Entry 中具体 media field |

**Original:** Example model:

```json
{
  "attributes": {
    "name": {
      "type": "string"
    },
    "cover": {
      "type": "media",
      "multiple": false
    }
  }
}
```

**中文译文:** 上述 schema 中，`cover` 是单文件 media field。上传时可同时传入 `ref`、`refId` 与 `field=cover`，让 file 直接关联到目标 Restaurant entry。

**Original:** You must send `FormData`.

**中文译文:** Entry file upload 同样必须使用 `FormData` request body。

## Update fileInfo

**Original:** `POST /api/upload?id=x` updates file metadata. `fileInfo` is the only accepted parameter.

**中文译文:** `POST /api/upload?id=x` 用于更新 file metadata，只接受 `fileInfo` parameter。

```js
import { FormData } from 'formdata-node';
import fetch from 'node-fetch';

const fileId = 50;
const newFileData = {
  alternativeText: 'My new alternative text for this image!',
};

const form = new FormData();
form.append('fileInfo', JSON.stringify(newFileData));

const response = await fetch(`http://localhost:1337/api/upload?id=${fileId}`, {
  method: 'post',
  body: form,
});
```

**中文译文:** 示例更新 file id 50 的 `alternativeText`。代码保持原样。

## Models definition

**Original:** Adding a file attribute to a model is like adding an association.

**中文译文:** 在 model 中添加 file/media attribute，本质上类似增加一个 association。

**Original:** A single media field uses `"type": "media", "multiple": false`; multiple media uses `"multiple": true`.

**中文译文:** 单文件 media field 使用 `"type": "media", "multiple": false`；多文件 media field 则设置 `"multiple": true`。Schema 中的其他 validation 规则（例如 `required`、`unique`）保持普通 model attribute 的定义方式。
