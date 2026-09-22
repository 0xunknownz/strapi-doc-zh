# 📖 对照翻译：Local Upload provider

> Source: `docusaurus/docs/cms/configurations/media-library-providers/local-upload.md`  
> Upstream SHA: `a4a3d1328d6701775796cc9f8b0c0d59779e8052`

**Original:** The `@strapi/provider-upload-local` package stores Media Library assets on the local server file system.

**中文译文:** `@strapi/provider-upload-local` 是 Strapi 官方 local upload provider，把 Media Library assets 存储在 Strapi server 的本地文件系统中。

## Installation

```bash
# Yarn
yarn add @strapi/provider-upload-local

# NPM
npm install @strapi/provider-upload-local --save
```

## Configuration

**Original:** Configure the provider in `/config/plugins.js|ts`.

**中文译文:** Local provider 同样在 `/config/plugins.js|ts` 的 `upload.config` 下配置。

**Original:** The local provider accepts a `sizeLimit` provider option in bytes; default is 1 GB.

**中文译文:** Local provider 的 `providerOptions` 当前主要支持：
- `sizeLimit`：单个 upload / replacement 最大文件大小；
- 单位为 bytes；
- 默认 `1000000000`，约 1 GB。

```js title="/config/plugins.js"
module.exports = ({ env }) => ({
  upload: {
    config: {
      provider: 'local',
      providerOptions: {
        sizeLimit: 100000,
      },
    },
  },
});
```

**Original:** When increasing `sizeLimit`, also increase the body-parser `maxFileSize`.

**中文译文:** 如果提高 provider 的 `sizeLimit`，还必须同步调整 body parser middleware 的 `maxFileSize`，否则 request 在到达 Upload provider 前就可能被 middleware 拒绝。

**Original:** Unlike S3 and Cloudinary, local upload requires no special security middleware settings.

**中文译文:** Local upload 的资源来自同一 origin，因此默认 security middleware 已允许 `'self'`，通常无需像 Cloudinary / S3 那样额外修改 CSP。
