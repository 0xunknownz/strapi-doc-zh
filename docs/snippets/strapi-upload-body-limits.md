# 📖 对照翻译：Upload body-size limits

> Source: `docusaurus/docs/snippets/strapi-upload-body-limits.md`  
> Upstream SHA: `bb46a6c34a81e868d8f267c2a1cd63bd0a5f2748`

**Original:** Uploaded files are limited by the Strapi body middleware's `formidable.maxFileSize`; `formLimit` and `jsonLimit` do not cap the file itself.

**中文译文:** Media upload 的文件大小主要受 `strapi::body` middleware 中的 `formidable.maxFileSize` 限制；`formLimit`、`jsonLimit`、`textLimit` 只限制普通 form / JSON / text body，并不直接控制上传文件本体。

```js title="/config/middlewares.js"
module.exports = [
  {
    name: 'strapi::body',
    config: {
      formLimit: '100mb',
      jsonLimit: '100mb',
      textLimit: '100mb',
      formidable: {
        maxFileSize: 100 * 1024 * 1024,
      },
    },
  },
];
```

**Original:** Upload providers have a separate `sizeLimit`, default 1 GB for local provider.

**中文译文:** Media Library provider 自身还可能有独立 `sizeLimit`。Proxy limit、body middleware limit、provider limit 三者中**最小值**决定实际可上传的最大文件。
