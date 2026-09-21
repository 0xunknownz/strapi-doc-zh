# 📖 对照翻译：Middleware Configuration for Strapi Cloud

> Source: `docusaurus/docs/cloud/advanced/middlewares.md`  
> Upstream SHA: `b4127704e9ee16a31113198725e3311f0f6bfd88`

**Original:** Middleware Configuration for Strapi Cloud

**中文译文:** Strapi Cloud Middleware 配置

**Original:** On Strapi Cloud, middleware customizations must go in `config/env/production/middlewares`. Changes to the global config file are overwritten on deploy.

**中文译文:** 在 Strapi Cloud 中，自定义 middleware 必须写在 `config/env/production/middlewares`。对全局配置文件的修改会在 deployment 时被覆盖。

**Original:** Prerequisites:

- A local Strapi project.
- A Strapi Cloud project.

**中文译文:** 前置条件：

- 一个本地 Strapi 项目；
- 一个 Strapi Cloud 项目，参阅 [Getting Started](/cloud/getting-started/deployment)。

**Original:** On Strapi Cloud, `NODE_ENV` is always set to `production`. The platform applies its own production-level middleware configuration on deploy. Any changes to the global `config/middlewares` file are overwritten and will not take effect. For available middleware options, see Middlewares configuration.

**中文译文:** 在 Strapi Cloud 中，`NODE_ENV` 始终设置为 `production`。平台会在 deployment 时应用自己的 production-level middleware 配置，因此对全局 `config/middlewares` 的任何修改都会被覆盖，无法生效。可用 middleware 选项请参阅 [Middlewares configuration](/cms/configurations/middlewares)。

**Original:** To apply custom middleware configuration on Strapi Cloud, place your changes in:

**中文译文:** 若要让自定义 middleware 配置在 Strapi Cloud 中生效，请把修改放到以下文件：

```text
# JavaScript
config/env/production/middlewares.js

# TypeScript
config/env/production/middlewares.ts
```

**Original:** The `config/env/production/middlewares` file **fully replaces** the global middleware array. Your file must include the complete list:

- `strapi::errors`
- `strapi::security`
- `strapi::cors`
- `strapi::poweredBy`
- `strapi::logger`
- `strapi::query`
- `strapi::body`
- `strapi::session`
- `strapi::favicon`
- `strapi::public`

Both CSP and CORS customizations can be combined in the same file.

**中文译文:** `config/env/production/middlewares` 会**完整替换**全局 middleware array，因此该文件必须包含完整列表：

- `strapi::errors`
- `strapi::security`
- `strapi::cors`
- `strapi::poweredBy`
- `strapi::logger`
- `strapi::query`
- `strapi::body`
- `strapi::session`
- `strapi::favicon`
- `strapi::public`

CSP 和 CORS 自定义配置可以放在同一个文件中。

**Original:** Notes:

- You can keep your existing `config/middlewares` file as-is as it will not cause conflicts. The production-specific file takes precedence on Strapi Cloud.
- Upload size limits on Strapi Cloud are enforced at the infrastructure level and cannot be overridden via the `strapi::body` config.
- For per-plan values and the memory-based recommendation for image uploads, see Upload size limits for Strapi Cloud. For external storage options, see Upload Provider Configuration.

**中文译文:** 注意：

- 可以保留现有 `config/middlewares`，不会产生冲突；在 Strapi Cloud 上，production-specific 文件优先级更高；
- Strapi Cloud 的 upload size limit 在基础设施层强制执行，无法通过 `strapi::body` 覆盖；
- 各方案限制以及基于内存的图片上传建议请参阅 [Upload size limits for Strapi Cloud](/cloud/advanced/upload-size-limits)；外部存储配置请参阅 [Upload Provider Configuration](/cloud/advanced/upload)。

## Custom Content Security Policy (CSP)

**Original:** If you use an external upload provider, allow its domain in the CSP directives. Without this, the Strapi Admin panel will block images and media from those sources.

**中文译文:** 如果使用外部 upload provider，需要在 CSP directives 中允许对应域名。否则，Strapi Admin panel 会阻止来自这些来源的图片与媒体资源。

**Original:** Create or update `config/env/production/middlewares`:

**中文译文:** 创建或更新 `config/env/production/middlewares`，完整示例如下，代码保持原样：

```js title="config/env/production/middlewares.js"
module.exports = [
  'strapi::errors',
  {
    name: 'strapi::security',
    config: {
      contentSecurityPolicy: {
        useDefaults: true,
        directives: {
          'connect-src': ["'self'", 'https:'],
          'img-src': [
            "'self'",
            'data:',
            'blob:',
            'market-assets.strapi.io',
            'your-custom-domain.com', // replace with your provider domain
          ],
          'media-src': [
            "'self'",
            'data:',
            'blob:',
            'market-assets.strapi.io',
            'your-custom-domain.com', // replace with your provider domain
          ],
          upgradeInsecureRequests: null,
        },
      },
    },
  },
  'strapi::cors',
  'strapi::poweredBy',
  'strapi::logger',
  'strapi::query',
  'strapi::body',
  'strapi::session',
  'strapi::favicon',
  'strapi::public',
];
```

```ts title="config/env/production/middlewares.ts"
export default [
  'strapi::errors',
  {
    name: 'strapi::security',
    config: {
      contentSecurityPolicy: {
        useDefaults: true,
        directives: {
          'connect-src': ["'self'", 'https:'],
          'img-src': [
            "'self'",
            'data:',
            'blob:',
            'market-assets.strapi.io',
            'your-custom-domain.com', // replace with your provider domain
          ],
          'media-src': [
            "'self'",
            'data:',
            'blob:',
            'market-assets.strapi.io',
            'your-custom-domain.com', // replace with your provider domain
          ],
          upgradeInsecureRequests: null,
        },
      },
    },
  },
  'strapi::cors',
  'strapi::poweredBy',
  'strapi::logger',
  'strapi::query',
  'strapi::body',
  'strapi::session',
  'strapi::favicon',
  'strapi::public',
];
```

**Original:** For a full list of upload providers and their required domains, see the Strapi Community Hub.

**中文译文:** 如需查看 upload provider 以及它们所需域名的完整列表，请参阅 [Strapi Community Hub](https://community.strapi.io/marketplace)。

## Custom CORS headers

**Original:** If your frontend sends custom request headers (e.g. for authorization flows), you need to explicitly allow them in the CORS configuration. Placing this in the global `config/middlewares` file will not work on Strapi Cloud. Place it in `config/env/production/middlewares` instead.

**中文译文:** 如果前端会发送自定义 request header，例如用于 authorization flow，就需要在 CORS 配置中显式允许这些 header。把配置写在全局 `config/middlewares` 中不会在 Strapi Cloud 生效，应写入 `config/env/production/middlewares`。

**Original:** Example CORS configuration:

**中文译文:** CORS 配置示例如下，代码保持原样：

```js title="config/env/production/middlewares.js"
module.exports = ({ env }) => [
  'strapi::errors',
  'strapi::security',
  {
    name: 'strapi::cors',
    config: {
      enabled: true,
      origin: [env('CLIENT_URL')],
      headers: [
        'Content-Type',
        'Authorization',
        'Origin',
        'Accept',
        'X-Requested-With',
        'your-custom-header', // add any custom headers your frontend sends
      ],
    },
  },
  'strapi::poweredBy',
  'strapi::logger',
  'strapi::query',
  'strapi::body',
  'strapi::session',
  'strapi::favicon',
  'strapi::public',
];
```

```ts title="config/env/production/middlewares.ts"
export default ({ env }) => [
  'strapi::errors',
  'strapi::security',
  {
    name: 'strapi::cors',
    config: {
      enabled: true,
      origin: [env('CLIENT_URL')],
      headers: [
        'Content-Type',
        'Authorization',
        'Origin',
        'Accept',
        'X-Requested-With',
        'your-custom-header', // add any custom headers your frontend sends
      ],
    },
  },
  'strapi::poweredBy',
  'strapi::logger',
  'strapi::query',
  'strapi::body',
  'strapi::session',
  'strapi::favicon',
  'strapi::public',
];
```
