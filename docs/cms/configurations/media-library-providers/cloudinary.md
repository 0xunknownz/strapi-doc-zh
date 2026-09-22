# 📖 对照翻译：Cloudinary provider

> Source: `docusaurus/docs/cms/configurations/media-library-providers/cloudinary.md`  
> Upstream SHA: `989617951c77c8e4e286d777de0610c0e009df52`

**Original:** The `@strapi/provider-upload-cloudinary` package stores Media Library assets on Cloudinary. Configure it with your Cloudinary cloud name, API key, and API secret.

**中文译文:** `@strapi/provider-upload-cloudinary` 是 Strapi 官方维护的 Media Library Cloudinary provider，用于把上传的 media assets 存储到 Cloudinary。配置时需要 Cloudinary cloud name、API key 与 API secret。

## Installation

```bash
# Yarn
yarn add @strapi/provider-upload-cloudinary

# NPM
npm install @strapi/provider-upload-cloudinary --save
```

## Configuration

**Original:** Provider configuration is defined in `/config/plugins.js|ts`.

**中文译文:** Media Library provider 配置写在 `/config/plugins.js|ts` 的 `upload.config` 中。

**Original:** Main keys are `provider`, `providerOptions`, and `actionOptions`.

**中文译文:**
- `provider`：provider name，这里为 `cloudinary`；
- `providerOptions`：初始化 provider 时传给 Cloudinary SDK 的配置；
- `actionOptions`：分别传给 `upload`、`uploadStream`、`delete` 等具体动作。

**Original code (kept unchanged):**

```js title="/config/plugins.js"
module.exports = ({ env }) => ({
  upload: {
    config: {
      provider: 'cloudinary',
      providerOptions: {
        cloud_name: env('CLOUDINARY_NAME'),
        api_key: env('CLOUDINARY_KEY'),
        api_secret: env('CLOUDINARY_SECRET'),
      },
      actionOptions: {
        upload: {},
        uploadStream: {},
        delete: {},
      },
    },
  },
});
```

**中文译文:** 建议把 Cloudinary credentials 放在 environment variables 中，而不是直接写入 source code。

## Security and environment notes

**Original:** Strapi's default security middleware only allows loading media from `'self'`.

**中文译文:** Strapi 默认 `strapi::security` middleware 的 Content Security Policy 很严格，media source 默认只允许 `'self'`。使用 Cloudinary / S3 等外部 provider 时，通常还需要调整 CSP，允许对应 CDN / provider domain。

**Original:** When different environments use different providers, configure them under `/config/env/<environment>/plugins.js|ts`.

**中文译文:** 如果 development / staging / production 使用不同 upload provider，应把对应配置放在 `/config/env/<environment>/plugins.js|ts`，避免在同一份 config 中硬编码 environment-specific provider。
