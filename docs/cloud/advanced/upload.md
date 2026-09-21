# 📖 对照翻译：Upload Provider Configuration for Strapi Cloud

> Source: `docusaurus/docs/cloud/advanced/upload.md`  
> Upstream SHA: `541317aba5e2ab61fc2f57a8e6e9063b16f29910`

**Original:** Upload Provider Configuration for Strapi Cloud

**中文译文:** Strapi Cloud Upload Provider 配置

**Original:** External storage like S3 or Cloudinary requires plugin setup, security middleware, and Cloud variables.

**中文译文:** 使用 Amazon S3、Cloudinary 等外部存储，需要完成 provider plugin、security middleware 以及 Cloud environment variables 的配置。

**Original:** Strapi Cloud comes with a local upload provider out of the box. However, it can also be configured to use a third-party upload provider, if needed.

**中文译文:** Strapi Cloud 默认提供本地 upload provider。如有需要，也可以配置为使用第三方 upload provider。

**Original:** For the file size and memory-based limits that apply to uploads, see Upload size limits for Strapi Cloud.

**中文译文:** 关于上传文件大小以及基于内存的限制，请参阅 [Upload size limits for Strapi Cloud](/cloud/advanced/upload-size-limits)。

## Configuring a third-party upload provider

**Original:** Please be advised that Strapi is unable to provide support for third-party upload providers.

**中文译文:** 请注意，Strapi 无法为第三方 upload provider 提供支持服务。

**Original:** Prerequisites:

- A local Strapi project running on `v4.8.2+`.
- Credentials for a third-party upload provider.

**中文译文:** 前置条件：

- 本地 Strapi 项目运行在 `v4.8.2+`；
- 拥有第三方 upload provider 的凭据，可在 [Strapi Community Hub](https://community.strapi.io/marketplace) 查找可用 provider。

**Original:** Configuring a third-party upload provider for use with Strapi Cloud requires the following 4 configuration steps, followed by a deployment:

1. Install the provider plugin in your local Strapi project.
2. Configure the provider in your local Strapi project.
3. Configure the security middleware in your local Strapi project.
4. Add environment variables to the Strapi Cloud project.

**中文译文:** 在 Strapi Cloud 中使用第三方 upload provider，需要先完成以下 4 个配置步骤，然后再部署：

1. 在本地 Strapi 项目中安装 provider plugin；
2. 在本地 Strapi 项目中配置 provider；
3. 在本地 Strapi 项目中配置 security middleware；
4. 向 Strapi Cloud 项目添加 environment variables。

### Install the provider plugin

**Original:** Using either `npm` or `yarn`, install the provider plugin in your local Strapi project as a package dependency by following the instructions in the respective entry for that provider in the Marketplace.

**中文译文:** 使用 `npm` 或 `yarn`，按照 [Marketplace](https://community.strapi.io/marketplace) 中对应 provider 的说明，把 provider plugin 作为 package dependency 安装到本地 Strapi 项目。

### Configure the provider

**Original:** To configure a third-party upload provider in your Strapi project, create or edit the plugins configuration file for your production environment `/config/env/production/plugins.js|ts` by adding upload configuration options as follows:

**中文译文:** 若要在 Strapi 项目中配置第三方 upload provider，请创建或编辑 production environment 的 plugins 配置文件 `/config/env/production/plugins.js|ts`，并按下面的结构加入 upload 配置。

**Original code (kept unchanged):**

```js title=/config/env/production/plugins.js
module.exports = ({ env }) => ({
// … some unrelated plugins configuration options
// highlight-start
upload: {
   config: {
      // … provider-specific upload configuration options go here
   }
// highlight-end
// … some other unrelated plugins configuration options
}
});
```

```ts title=/config/env/production/plugins.ts
export default ({ env }) => ({
// … some unrelated plugins configuration options
// highlight-start
upload: {
   config: {
      // … provider-specific upload configuration options go here
   }
// highlight-end
// … some other unrelated plugins configuration options
}
});
```

**中文译文:** JavaScript 与 TypeScript 的配置结构相同，在 `upload.config` 中填写 provider 对应选项即可。代码保持原样。

**Original:** The file structure must match the above path exactly, or the configuration will not be applied to Strapi Cloud.

**中文译文:** 文件路径必须与上面完全一致，否则配置不会应用到 Strapi Cloud。

**Original:** Each provider will have different configuration settings available. Review the respective entry for that provider in the Marketplace.

**中文译文:** 不同 provider 支持的配置项不同，请参阅 [Marketplace](https://community.strapi.io/marketplace) 中对应 provider 的说明。

### Cloudinary examples

**Original code (kept unchanged):**

```js title=/config/env/production/plugins.js
module.exports = ({ env }) => ({
  // ...
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
  // ...
});
```

```ts title=/config/env/production/plugins.ts
export default ({ env }) => ({
  // ...
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
  // ...
});
```

**中文译文:** 上面分别是 Cloudinary 的 JavaScript 和 TypeScript 配置示例。代码保持原样。

### Amazon S3 examples

**Original:** For full S3 provider configuration details (credential formats, extended options, S3-compatible services), see the Amazon S3 provider page in the CMS documentation.

**中文译文:** 关于 S3 provider 的完整配置说明，包括 credential 格式、扩展选项和 S3-compatible services，请参阅 CMS 文档中的 [Amazon S3 provider](/cms/configurations/media-library-providers/amazon-s3)。

**Original code (kept unchanged):**

```js title=/config/env/production/plugins.js
module.exports = ({ env }) => ({
  // ...
  upload: {
    config: {
      provider: 'aws-s3',
      providerOptions: {
        baseUrl: env('CDN_URL'),
        rootPath: env('CDN_ROOT_PATH'),
        s3Options: {
          credentials: {
            accessKeyId: env('AWS_ACCESS_KEY_ID'),
            secretAccessKey: env('AWS_ACCESS_SECRET'),
          },
          region: env('AWS_REGION'),
          params: {
            ACL: env('AWS_ACL', 'public-read'),
            signedUrlExpires: env('AWS_SIGNED_URL_EXPIRES', 15 * 60),
            Bucket: env('AWS_BUCKET'),
          },
        },
      },
      actionOptions: {
        upload: {},
        uploadStream: {},
        delete: {},
      },
    },
  },
  // ...
});
```

```ts title=/config/env/production/plugins.ts
export default ({ env }) => ({
  // ...
  upload: {
    config: {
      provider: 'aws-s3',
      providerOptions: {
        baseUrl: env('CDN_URL'),
        rootPath: env('CDN_ROOT_PATH'),
        s3Options: {
          credentials: {
            accessKeyId: env('AWS_ACCESS_KEY_ID'),
            secretAccessKey: env('AWS_ACCESS_SECRET'),
          },
          region: env('AWS_REGION'),
          params: {
            ACL: env('AWS_ACL', 'public-read'),
            signedUrlExpires: env('AWS_SIGNED_URL_EXPIRES', 15 * 60),
            Bucket: env('AWS_BUCKET'),
          },
        },
      },
      actionOptions: {
        upload: {},
        uploadStream: {},
        delete: {},
      },
    },
  },
  // ...
});
```

**中文译文:** 上面分别是 Amazon S3 的 JavaScript 与 TypeScript 配置示例。代码保持原样。

### Configure the security middleware

**Original:** Due to the default settings in the Strapi security middleware you will need to modify the `contentSecurityPolicy` settings to properly see thumbnail previews in the Media Library.

**中文译文:** 由于 Strapi security middleware 的默认设置，要在 Media Library 中正常显示 thumbnail preview，需要修改 `contentSecurityPolicy`。

**Original:** On Strapi Cloud, `NODE_ENV` is always set to `production`. Changes to the global `config/middlewares.ts` file are overwritten on each deploy and will not take effect. Place your Security Middleware customizations in `config/env/production/middlewares.ts` instead.

**中文译文:** 在 Strapi Cloud 中，`NODE_ENV` 始终为 `production`。对全局 `config/middlewares.ts` 的修改会在每次 deployment 时被覆盖，不会生效。应将 Security Middleware 自定义内容放在 `config/env/production/middlewares.ts`。详情请参阅 [Middleware Configuration for Strapi Cloud](/cloud/advanced/middlewares)。

**Original:** To do this in your Strapi project:

1. Navigate to `/config/env/production/middlewares.js` or `/config/env/production/middlewares.ts` in your Strapi project.
2. Replace the default `strapi::security` string with the object provided by the upload provider.

**中文译文:** 在 Strapi 项目中按以下步骤操作：

1. 打开 `/config/env/production/middlewares.js` 或 `/config/env/production/middlewares.ts`；
2. 将默认的 `strapi::security` 字符串替换为 upload provider 所要求的配置对象。

### Cloudinary CSP examples

**Original code (kept unchanged):**

```js title=/config/env/production/middlewares.js
module.exports = [
  // ...
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
            'res.cloudinary.com'
          ],
          'media-src': [
            "'self'",
            'data:',
            'blob:',
            'market-assets.strapi.io',
            'res.cloudinary.com',
          ],
          upgradeInsecureRequests: null,
        },
      },
    },
  },
  // ...
];
```

```ts title=/config/env/production/middlewares.ts
export default [
  // ...
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
            'res.cloudinary.com'
          ],
          'media-src': [
            "'self'",
            'data:',
            'blob:',
            'market-assets.strapi.io',
            'res.cloudinary.com',
          ],
          upgradeInsecureRequests: null,
        },
      },
    },
  },
  // ...
];
```

**中文译文:** Cloudinary 的 CSP 配置需要允许 `res.cloudinary.com`。以上代码保持原样。

### Amazon S3 CSP examples

**Original code (kept unchanged):**

```js title=/config/env/production/middlewares.js
module.exports = [
  // ...
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
            'yourBucketName.s3.yourRegion.amazonaws.com',
          ],
          'media-src': [
            "'self'",
            'data:',
            'blob:',
            'market-assets.strapi.io',
            'yourBucketName.s3.yourRegion.amazonaws.com',
          ],
          upgradeInsecureRequests: null,
        },
      },
    },
  },
  // ...
];
```

```ts title=/config/env/production/middlewares.ts
export default [
  // ...
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
            'yourBucketName.s3.yourRegion.amazonaws.com',
          ],
          'media-src': [
            "'self'",
            'data:',
            'blob:',
            'market-assets.strapi.io',
            'yourBucketName.s3.yourRegion.amazonaws.com',
          ],
          upgradeInsecureRequests: null,
        },
      },
    },
  },
  // ...
];
```

**中文译文:** Amazon S3 的 CSP 配置需要允许对应 bucket domain。请把 `yourBucketName.s3.yourRegion.amazonaws.com` 替换为实际域名。代码保持原样。

**Original:** Before pushing the above changes to GitHub, add environment variables to the Strapi Cloud project to prevent triggering a rebuild and new deployment of the project before the changes are complete.

**中文译文:** 在把上述变更 push 到 GitHub 之前，请先向 Strapi Cloud 项目添加 environment variables，以免配置尚未完成时提前触发 rebuild 与新 deployment。

### Strapi Cloud configuration

**Original:** 1. Log into Strapi Cloud and click on the corresponding project on the Projects page.
2. Click on the **Settings** tab and choose **Variables** in the left menu.
3. Add the required environment variables specific to the upload provider.
4. Click **Save**.

**中文译文:** 1. 登录 Strapi Cloud，在 *Projects* 页面进入目标项目。  
2. 打开 **Settings**，在左侧菜单选择 **Variables**。  
3. 添加当前 upload provider 所需的 environment variables。  
4. 点击 **Save**。

**Original:** Cloudinary environment variables:

| Variable | Value |
|---|---|
| `CLOUDINARY_NAME` | your_cloudinary_name |
| `CLOUDINARY_KEY` | your_cloudinary_api_key |
| `CLOUDINARY_SECRET` | your_cloudinary_secret |

**中文译文:** Cloudinary environment variables：

| Variable | Value |
|---|---|
| `CLOUDINARY_NAME` | your_cloudinary_name |
| `CLOUDINARY_KEY` | your_cloudinary_api_key |
| `CLOUDINARY_SECRET` | your_cloudinary_secret |

**Original:** Amazon S3 environment variables:

| Variable | Value |
|---|---|
| `AWS_ACCESS_KEY_ID` | your_aws_access_key_id |
| `AWS_ACCESS_SECRET` | your_aws_access_secret |
| `AWS_REGION` | your_aws_region |
| `AWS_BUCKET` | your_aws_bucket |
| `CDN_URL` | your_cdn_url |
| `CDN_ROOT_PATH` | your_cdn_root_path |

**中文译文:** Amazon S3 environment variables：

| Variable | Value |
|---|---|
| `AWS_ACCESS_KEY_ID` | your_aws_access_key_id |
| `AWS_ACCESS_SECRET` | your_aws_access_secret |
| `AWS_REGION` | your_aws_region |
| `AWS_BUCKET` | your_aws_bucket |
| `CDN_URL` | your_cdn_url |
| `CDN_ROOT_PATH` | your_cdn_root_path |

### Deployment

**Original:** To deploy the project and use the third-party upload provider, push the changes from earlier. This will trigger a rebuild and new deployment of the Strapi Cloud project.

**中文译文:** 要部署项目并使用第三方 upload provider，请 push 前面完成的变更。这会触发 Strapi Cloud 项目的 rebuild 和新的 deployment。

**Original:** Once the application finishes building, the project will use the new upload provider.

**中文译文:** 应用 build 完成后，项目就会开始使用新的 upload provider。

**Original:** If you want to create a custom upload provider, please refer to the Providers documentation in the CMS Documentation.

**中文译文:** 如果要创建自定义 upload provider，请参阅 CMS 文档中的 [Providers](/cms/features/media-library#providers)。
