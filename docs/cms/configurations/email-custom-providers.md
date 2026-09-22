# 📖 对照翻译：Creating custom email providers

> Source: `docusaurus/docs/cms/configurations/email-custom-providers.md`  
> Upstream SHA: `81c143ca4835a2855162ad1918ddaf36b10a131c`

**Original:** Build a custom email provider by exporting a Node.js module with a `send()` function. Use it locally or publish it to npm.

**中文译文:** Strapi Email feature 把实际发送动作委托给 provider。没有合适的官方 / community provider 时，可以实现自己的 Node.js module，并在 provider 中暴露标准 `send()` interface。

## Provider interface

**Original:** A provider module exports `init(providerOptions, settings)`, which returns an object containing `send(options)`.

**中文译文:** Custom provider 必须 export `init()`。该函数接收 `providerOptions` 与 `settings`，并返回至少包含 `send(options)` 的 object。

```js
module.exports = {
  init: (providerOptions = {}, settings = {}) => {
    return {
      send: async options => {},
    };
  },
};
```

**Original:** Inside `send`, you can access provider options, settings, and call-specific options.

**中文译文:**
- `providerOptions`：来自 `/config/plugins.js|ts` 中 provider-specific 配置；
- `settings`：来自 Email feature settings；
- `options`：controller / service 调用 `send()` 时传入的具体邮件参数。

**Original:** Strapi-maintained providers can be used as implementation references.

**中文译文:** 可以参考 Strapi 官方 provider source，了解错误处理、credential mapping 与 transport client 初始化模式。

## Publishing to npm

**Original:** Publish the provider to npm and configure it like other providers.

**中文译文:** 如果需要复用 / 分享，可以把 provider 发布到 npm；安装后按普通 Email provider 方式在 `config/plugins` 配置。

## Using a local provider

**Original:** A local provider can live under `providers/strapi-provider-email-custom` and be linked through `package.json`.

**中文译文:** 不发布 npm 时，可以把 provider 作为 local package 放在 project root，例如：
`providers/strapi-provider-email-custom`

然后在 `package.json` 中通过 file dependency 引用：

```json
{
  "dependencies": {
    "strapi-provider-email-custom": "file:providers/strapi-provider-email-custom"
  }
}
```

**Original:** Configure it in `/config/plugins.js|ts`, then run `yarn` or `npm install`.

**中文译文:** 完成 local dependency 后，在 `/config/plugins.js|ts` 配置 provider，并重新运行 `yarn` / `npm install` 建立 package link。
