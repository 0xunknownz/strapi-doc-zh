# 📖 对照翻译：Email Providers configuration for Strapi Cloud

> Source: `docusaurus/docs/cloud/advanced/email.md`  
> Upstream SHA: `a0889c435cf68f065af87744357ad7cd2732e757`

**Original:** Email Providers configuration for Strapi Cloud

**中文译文:** Strapi Cloud 的 Email Provider 配置

**Original:** Third‑party email services integrate through plugins and environment variables to replace the default sender.

**中文译文:** 可以通过插件与 environment variables 集成第三方 email service，以替换默认邮件发送服务。

**Original:** Strapi Cloud comes with a basic email provider out of the box. However, it can also be configured to utilize another email provider, if needed.

**中文译文:** Strapi Cloud 默认提供一个基础 email provider。如有需要，也可以配置为使用其他 email provider。

**Original:** Please be advised that Strapi is unable to provide support for third-party email providers.

**中文译文:** 请注意，Strapi 无法为第三方 email provider 提供支持服务。

**Original:** Prerequisites:

- A local Strapi project running on `v4.8.2+`.
- Credentials for another email provider.

**中文译文:** 前置条件：

- 本地 Strapi 项目运行在 `v4.8.2+`；
- 拥有其他 email provider 的凭据，可从 [Strapi Community Hub](https://community.strapi.io/marketplace) 查找可用 provider。

## Configuration

**Original:** Configuring another email provider for use with Strapi Cloud requires 3 steps:

1. Install the provider plugin in your local Strapi project.
2. Configure the provider in your local Strapi project.
3. Add environment variables to the Strapi Cloud project.

**中文译文:** 在 Strapi Cloud 中使用其他 email provider，需要完成 3 个步骤：

1. 在本地 Strapi 项目中安装 provider plugin；
2. 在本地 Strapi 项目中配置 provider；
3. 向 Strapi Cloud 项目添加 environment variables。

### Install the Provider Plugin

**Original:** Using either `npm` or `yarn`, install the provider plugin in your local Strapi project as a package dependency by following the instructions in the respective entry for that provider in the Marketplace.

**中文译文:** 使用 `npm` 或 `yarn`，按照 [Marketplace](https://community.strapi.io/marketplace) 中对应 provider 的说明，把 provider plugin 作为 package dependency 安装到本地 Strapi 项目中。

### Configure the Provider

**Original:** In your Strapi project, create a `/config/env/production/plugins.js` or `/config/env/production/plugins.ts` file with the following content:

**中文译文:** 在 Strapi 项目中创建 `/config/env/production/plugins.js` 或 `/config/env/production/plugins.ts`，并按下面的结构配置：

**Original code (kept unchanged):**

```js title=/config/env/production/plugins.js
module.exports = ({ env }) => ({
  // … some unrelated plugins configuration options
  // highlight-start
  email: {
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
  email: {
    config: {
        // … provider-specific upload configuration options go here
    }
  // highlight-end
  // … some other unrelated plugins configuration options
  }
});
```

**中文译文:** JavaScript 与 TypeScript 的配置结构相同，只需在 `email.config` 中填写 provider 对应的配置。代码保持原样。

**Original:** The file structure must match the above path exactly, or the configuration will not be applied to Strapi Cloud.

**中文译文:** 文件路径必须与上面完全一致，否则配置不会应用到 Strapi Cloud。

**Original:** Each provider will have different configuration settings available. Review the respective entry for that provider in the Marketplace.

**中文译文:** 不同 provider 支持的配置项不同，请参阅 [Marketplace](https://community.strapi.io/marketplace) 中对应 provider 的说明。

**Original:** Example configurations for Sendgrid, Amazon SES, and Mailgun:

**中文译文:** 以下为 SendGrid、Amazon SES 和 Mailgun 的示例配置。代码保持原样。

```js title=/config/env/production/plugins.js
// Sendgrid
module.exports = ({ env }) => ({
  email: {
    config: {
      provider: 'sendgrid',
      providerOptions: {
        apiKey: env('SENDGRID_API_KEY'),
      },
      settings: {
        defaultFrom: 'myemail@protonmail.com',
        defaultReplyTo: 'myemail@protonmail.com',
      },
    },
  },
});
```

```js title=/config/env/production/plugins.js
// Amazon SES
module.exports = ({ env }) => ({
  email: {
    config: {
      provider: 'amazon-ses',
      providerOptions: {
        key: env('AWS_SES_KEY'),
        secret: env('AWS_SES_SECRET'),
        amazon: 'https://email.us-east-1.amazonaws.com',
      },
      settings: {
        defaultFrom: 'myemail@protonmail.com',
        defaultReplyTo: 'myemail@protonmail.com',
      },
    },
  },
});
```

```js title=/config/env/production/plugins.js
// Mailgun
module.exports = ({ env }) => ({
  email: {
    config: {
      provider: 'mailgun',
      providerOptions: {
        key: env('MAILGUN_API_KEY'), // Required
        domain: env('MAILGUN_DOMAIN'), // Required
        url: env('MAILGUN_URL', 'https://api.mailgun.net'), //Optional. If domain region is Europe use 'https://api.eu.mailgun.net'
      },
      settings: {
        defaultFrom: 'myemail@protonmail.com',
        defaultReplyTo: 'myemail@protonmail.com',
      },
    },
  },
});
```

```ts title=/config/env/production/plugins.ts
// Sendgrid
export default ({ env }) => ({
  email: {
    config: {
      provider: 'sendgrid',
      providerOptions: {
        apiKey: env('SENDGRID_API_KEY'),
      },
      settings: {
        defaultFrom: 'myemail@protonmail.com',
        defaultReplyTo: 'myemail@protonmail.com',
      },
    },
  },
});
```

```ts title=/config/env/production/plugins.ts
// Amazon SES
export default ({ env }) => ({
  email: {
    config: {
      provider: 'amazon-ses',
      providerOptions: {
        key: env('AWS_SES_KEY'),
        secret: env('AWS_SES_SECRET'),
        amazon: 'https://email.us-east-1.amazonaws.com',
      },
      settings: {
        defaultFrom: 'myemail@protonmail.com',
        defaultReplyTo: 'myemail@protonmail.com',
      },
    },
  },
});
```

```ts title=/config/env/production/plugins.ts
// Mailgun
export default ({ env }) => ({
  email: {
    config: {
      provider: 'mailgun',
      providerOptions: {
        key: env('MAILGUN_API_KEY'), // Required
        domain: env('MAILGUN_DOMAIN'), // Required
        url: env('MAILGUN_URL', 'https://api.mailgun.net'), //Optional. If domain region is Europe use 'https://api.eu.mailgun.net'
      },
      settings: {
        defaultFrom: 'myemail@protonmail.com',
        defaultReplyTo: 'myemail@protonmail.com',
      },
    },
  },
});
```

**Original:** Before pushing the above changes to GitHub, add environment variables to the Strapi Cloud project to prevent triggering a rebuild and new deployment of the project before the changes are complete.

**中文译文:** 在把上述变更 push 到 GitHub 之前，建议先在 Strapi Cloud 项目中添加 environment variables，以免配置尚未完成就提前触发 rebuild 和新 deployment。

### Strapi Cloud Configuration

**Original:** 1. Log into Strapi Cloud and click on the corresponding project on the Projects page.
2. Click on the **Settings** tab and choose **Variables** in the left menu.
3. Add the required environment variables specific to the email provider.
4. Click **Save**.

**中文译文:** 1. 登录 Strapi Cloud，在 *Projects* 页面进入目标项目。  
2. 打开 **Settings**，在左侧菜单选择 **Variables**。  
3. 添加当前 email provider 所需的 environment variables。  
4. 点击 **Save**。

**Original:** Example environment variables:

| Provider | Variables |
|---|---|
| SendGrid | `SENDGRID_API_KEY` |
| Amazon SES | `AWS_SES_KEY`, `AWS_SES_SECRET` |
| Mailgun | `MAILGUN_API_KEY`, `MAILGUN_DOMAIN`, `MAILGUN_URL` |

**中文译文:** 示例 environment variables：

| Provider | Variables |
|---|---|
| SendGrid | `SENDGRID_API_KEY` |
| Amazon SES | `AWS_SES_KEY`、`AWS_SES_SECRET` |
| Mailgun | `MAILGUN_API_KEY`、`MAILGUN_DOMAIN`、`MAILGUN_URL` |

## Deployment

**Original:** To deploy the project and utilize another party email provider, push the changes from earlier. This will trigger a rebuild and new deployment of the Strapi Cloud project.

**中文译文:** 要部署项目并启用第三方 email provider，请 push 前面完成的变更。这会触发 Strapi Cloud 项目的 rebuild 和新的 deployment。

**Original:** Once the application finishes building, the project will use the new email provider.

**中文译文:** 应用 build 完成后，项目就会开始使用新的 email provider。

**Original:** If you want to create a custom email provider, please refer to the Email providers documentation in the CMS Documentation.

**中文译文:** 如果需要创建自定义 email provider，请参阅 CMS 文档中的 [Email providers](/cms/features/email#providers)。
