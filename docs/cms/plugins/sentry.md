# 📖 对照翻译：Sentry plugin

> Source: `docusaurus/docs/cms/plugins/sentry.md`  
> Upstream SHA: `c253b2fe9cad613dedfe6030bb2fc4da95a3eb1b`

**Original:** The Sentry plugin connects Strapi to Sentry to report errors and attach debugging metadata.

**中文译文:** `@strapi/plugin-sentry` 将 Strapi server 与 Sentry 集成，用于上报 application error、附加 debugging metadata，并在 server code 中暴露可复用的 Sentry service。

## Installation

```bash
# Yarn
yarn add @strapi/plugin-sentry

# NPM
npm install @strapi/plugin-sentry
```

## Configuration

| Property | Type | Default | 中文说明 |
|---|---|---|---|
| `dsn` | string | `null` | Sentry Data Source Name |
| `sendMetadata` | boolean | `true` | 是否附加 OS / browser 等辅助 metadata |
| `init` | object | `{}` | 直接传给 Sentry Node SDK 的 initialization options |

```js title="/config/plugins.js"
module.exports = ({ env }) => ({
  sentry: {
    enabled: true,
    config: {
      dsn: env('SENTRY_DSN'),
      sendMetadata: true,
    },
  },
});
```

**Original:** A nil DSN keeps the plugin/service available but prevents events from being sent.

**中文译文:** `enabled: true` 但 `dsn` 为 `null` / `undefined` 时，plugin 仍会注册，业务代码仍可调用 Sentry service，但不会真正发送 event。这样可以让 development / test 环境复用同一套代码。

```js
dsn:
  env('NODE_ENV') === 'production'
    ? env('SENTRY_DSN')
    : null,
```

## Disable completely

```js
sentry: {
  enabled: false,
}
```

**中文译文:** 完全 disable 后，plugin 不会加载，对应 service 也不可用。

## Usage

```js
const sentryService =
  strapi.plugin('sentry').service('sentry');
```

| Method | 中文说明 |
|---|---|
| `sendError(error, configureScope?)` | 手动发送 error，可选 callback 自定义 Sentry scope |
| `getInstance()` | 直接获得底层 Sentry SDK instance |

```js
try {
  // Your code
} catch (error) {
  strapi
    .plugin('sentry')
    .service('sentry')
    .sendError(error, (scope) => {
      scope.setTag('my_custom_tag', 'Tag value');
    });

  throw error;
}
```

**中文译文:** 示例在 catch 中上报 error，并添加 custom tag；之后重新抛出 error，保持原业务错误流程。
