# 📖 对照翻译：Advanced Nodemailer configuration

> Source: `docusaurus/docs/cms/configurations/email-nodemailer.md`  
> Upstream SHA: `90ed040eb380ffb573b3901722806473402e058d`

**Original:** The Nodemailer provider supports OAuth2 authentication, connection pooling, DKIM signing, and rate limiting. Each scenario adds specific keys to `providerOptions` on top of a standard SMTP configuration.

**中文译文:** Nodemailer provider 支持 OAuth2 authentication、connection pooling、DKIM signing 和 rate limiting。每种场景都是在标准 SMTP configuration 的 `providerOptions` 基础上增加对应配置项。

**Original:** This page covers production scenarios for the community `@strapi/provider-email-nodemailer` package used with the Email feature. For basic installation and SMTP setup, see Configuring providers.

**中文译文:** 本页介绍 community package `@strapi/provider-email-nodemailer` 在 production 中的高级配置，可与 Strapi [Email feature](/cms/features/email) 一起使用。基础 provider 安装与 SMTP setup 请参阅 [Configuring providers](/cms/features/email#configuring-providers)。

**Original:** For the full list of providerOptions, see the provider README on npm.

**中文译文:** 完整 `providerOptions` 列表请参阅 npm 上的 `@strapi/provider-email-nodemailer` README。

## OAuth2 authentication

**Original:** For Gmail or Outlook services that require OAuth2 instead of a password:

**中文译文:** 对 Gmail、Outlook 等要求 OAuth2 而不是普通 password authentication 的服务，可以在 `providerOptions.auth` 中设置 OAuth2 参数。

**Original code (kept unchanged):**

```js title="/config/plugins.js"
module.exports = ({ env }) => ({
  email: {
    config: {
      provider: 'nodemailer',
      providerOptions: {
        host: 'smtp.gmail.com',
        port: 465,
        secure: true,
        auth: {
          type: 'OAuth2',
          user: env('SMTP_USER'),
          clientId: env('OAUTH_CLIENT_ID'),
          clientSecret: env('OAUTH_CLIENT_SECRET'),
          refreshToken: env('OAUTH_REFRESH_TOKEN'),
        },
      },
      settings: {
        defaultFrom: env('SMTP_USER'),
        defaultReplyTo: env('SMTP_USER'),
      },
    },
  },
});
```

```ts title="/config/plugins.ts"
export default ({ env }) => ({
  email: {
    config: {
      provider: 'nodemailer',
      providerOptions: {
        host: 'smtp.gmail.com',
        port: 465,
        secure: true,
        auth: {
          type: 'OAuth2',
          user: env('SMTP_USER'),
          clientId: env('OAUTH_CLIENT_ID'),
          clientSecret: env('OAUTH_CLIENT_SECRET'),
          refreshToken: env('OAUTH_REFRESH_TOKEN'),
        },
      },
      settings: {
        defaultFrom: env('SMTP_USER'),
        defaultReplyTo: env('SMTP_USER'),
      },
    },
  },
});
```

**中文译文:** JavaScript 与 TypeScript 的 OAuth2 配置示例保持原样。

## Connection pooling

**Original:** Use connection pooling to reuse SMTP connections and improve throughput when sending many emails.

**中文译文:** 发送大量 email 时，可以使用 connection pooling 复用 SMTP connections，提高 throughput。

**Original code (kept unchanged):**

```js title="/config/plugins.js"
module.exports = ({ env }) => ({
  email: {
    config: {
      provider: 'nodemailer',
      providerOptions: {
        host: env('SMTP_HOST'),
        port: 465,
        secure: true,
        pool: true,
        maxConnections: 5,
        maxMessages: 100,
        auth: {
          user: env('SMTP_USERNAME'),
          pass: env('SMTP_PASSWORD'),
        },
      },
      settings: {
        defaultFrom: 'hello@example.com',
        defaultReplyTo: 'hello@example.com',
      },
    },
  },
});
```

```ts title="/config/plugins.ts"
export default ({ env }) => ({
  email: {
    config: {
      provider: 'nodemailer',
      providerOptions: {
        host: env('SMTP_HOST'),
        port: 465,
        secure: true,
        pool: true,
        maxConnections: 5,
        maxMessages: 100,
        auth: {
          user: env('SMTP_USERNAME'),
          pass: env('SMTP_PASSWORD'),
        },
      },
      settings: {
        defaultFrom: 'hello@example.com',
        defaultReplyTo: 'hello@example.com',
      },
    },
  },
});
```

**中文译文:** `pool: true` 启用 connection pool；`maxConnections` 控制最大并发 connections，`maxMessages` 控制单 connection 可发送的最大消息数。代码保持原样。

## DKIM signing

**Original:** Add DKIM signatures to improve deliverability and authenticate outbound mail.

**中文译文:** 可以为 outbound mail 添加 DKIM signature，以提升 deliverability 并验证邮件来源。

**Original code (kept unchanged):**

```js title="/config/plugins.js"
module.exports = ({ env }) => ({
  email: {
    config: {
      provider: 'nodemailer',
      providerOptions: {
        host: env('SMTP_HOST'),
        port: 587,
        auth: {
          user: env('SMTP_USERNAME'),
          pass: env('SMTP_PASSWORD'),
        },
        dkim: {
          domainName: 'example.com',
          keySelector: 'mail',
          privateKey: env('DKIM_PRIVATE_KEY'),
        },
      },
      settings: {
        defaultFrom: 'hello@example.com',
        defaultReplyTo: 'hello@example.com',
      },
    },
  },
});
```

```ts title="/config/plugins.ts"
export default ({ env }) => ({
  email: {
    config: {
      provider: 'nodemailer',
      providerOptions: {
        host: env('SMTP_HOST'),
        port: 587,
        auth: {
          user: env('SMTP_USERNAME'),
          pass: env('SMTP_PASSWORD'),
        },
        dkim: {
          domainName: 'example.com',
          keySelector: 'mail',
          privateKey: env('DKIM_PRIVATE_KEY'),
        },
      },
      settings: {
        defaultFrom: 'hello@example.com',
        defaultReplyTo: 'hello@example.com',
      },
    },
  },
});
```

**中文译文:** DKIM 配置通过 `domainName`、`keySelector` 和 `DKIM_PRIVATE_KEY` 指定签名信息。代码保持原样。

## Rate limiting

**Original:** Limit messages per interval to avoid triggering spam filters.

**中文译文:** 可以限制单位时间内发送的 message 数量，降低触发 spam filter 的风险。

**Original code (kept unchanged):**

```js title="/config/plugins.js"
module.exports = ({ env }) => ({
  email: {
    config: {
      provider: 'nodemailer',
      providerOptions: {
        host: env('SMTP_HOST'),
        port: 465,
        secure: true,
        pool: true,
        rateLimit: 5,
        rateDelta: 1000,
        auth: {
          user: env('SMTP_USERNAME'),
          pass: env('SMTP_PASSWORD'),
        },
      },
      settings: {
        defaultFrom: 'hello@example.com',
        defaultReplyTo: 'hello@example.com',
      },
    },
  },
});
```

```ts title="/config/plugins.ts"
export default ({ env }) => ({
  email: {
    config: {
      provider: 'nodemailer',
      providerOptions: {
        host: env('SMTP_HOST'),
        port: 465,
        secure: true,
        pool: true,
        rateLimit: 5,
        rateDelta: 1000,
        auth: {
          user: env('SMTP_USERNAME'),
          pass: env('SMTP_PASSWORD'),
        },
      },
      settings: {
        defaultFrom: 'hello@example.com',
        defaultReplyTo: 'hello@example.com',
      },
    },
  },
});
```

**中文译文:** 该示例将 `rateLimit` 设为 5、`rateDelta` 设为 1000ms，即每秒最多 5 条 message。代码保持原样。

**Original:** `rateLimit` and `rateDelta` only take effect when `pool: true`.

**中文译文:** `rateLimit` 与 `rateDelta` 只有在同时设置 `pool: true` 时才会生效。
