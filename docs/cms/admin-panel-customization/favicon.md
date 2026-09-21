# 📖 对照翻译：Favicon

> Source: `docusaurus/docs/cms/admin-panel-customization/favicon.md`  
> Upstream SHA: `44f743753e147d098120a1f7bedc83cf660ecac5`

**Original:** Replace the Strapi admin panel favicon by replacing the `favicon.png` file at the project root or configuring the `strapi::favicon` middleware, then rebuild the app.

**中文译文:** 可以通过替换 project root 的 `favicon.png`，或配置 `strapi::favicon` middleware，更换 Strapi admin panel favicon；修改后需要重新 build admin app。

**Original:** Replacing branding assets lets the interface match your identity.

**中文译文:** Favicon 与 [logos](/cms/admin-panel-customization/logos) 都属于 branding customization，可让 admin panel 与产品视觉身份一致。

## Approaches

**Original:** Approach 1: replace `favicon.png` in project root.

**中文译文:** 方法 1：直接替换 Strapi project root 中的 `favicon.png`。

**Original:** Approach 2: configure `strapi::favicon`.

```js title="/config/middlewares.js"
{
  name: 'strapi::favicon',
  config: {
    path: 'my-custom-favicon.png',
  },
},
```

**中文译文:** 方法 2：在 middleware configuration 中设置 `strapi::favicon.config.path`。代码保持原样。

**Original:** Rebuild and run with `yarn build && yarn develop`.

**中文译文:** 修改后运行 `yarn build && yarn develop`（或对应 npm command）重新 build 并启动。

**Original:** Clear browser/CDN favicon caches.

**中文译文:** 如果仍看到旧 favicon，请清理 browser cache，以及 Cloudflare 等 CDN / domain management layer 的 cache。
