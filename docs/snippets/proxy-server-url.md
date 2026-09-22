# 📖 对照翻译：Public URL behind a reverse proxy

> Source: `docusaurus/docs/snippets/proxy-server-url.md`  
> Upstream SHA: `da7ebcb32706a45838de9be18774518bd1215639`

**Original:** The `url` option in server configuration defines the public address of your application. Strapi uses it for password-reset links, third-party login callbacks, and media asset URLs.

**中文译文:** Server configuration 中的 `url` 定义 Strapi application 对外公开地址。Strapi 会用它生成 password reset link、第三方 login provider callback URL、media asset absolute URL 等。

**Original code (kept unchanged):**

```js title="/config/server.js"
module.exports = ({ env }) => ({
  host: env('HOST', '0.0.0.0'),
  port: env.int('PORT', 1337),
  url: env('PUBLIC_URL', 'https://api.example.com'),
  app: {
    keys: env.array('APP_KEYS'),
  },
});
```

**中文译文:** `PUBLIC_URL` 应设置为真实用户访问的 public origin，而不是 `localhost:1337`。
