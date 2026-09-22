# 📖 对照翻译：Trust reverse-proxy headers

> Source: `docusaurus/docs/snippets/proxy-trust-headers.md`  
> Upstream SHA: `8e9796051320b2e623bc1f92b03dbe9c227995d0`

**Original:** Enable proxy support through `server.proxy` so Strapi can trust `X-Forwarded-*` headers.

**中文译文:** 通过 `server.proxy` 启用 reverse-proxy support 后，Strapi 才会从 `X-Forwarded-*` headers 读取 client IP、protocol 与 host，而不是使用 proxy socket address。

```js title="/config/server.js"
module.exports = ({ env }) => ({
  host: env('HOST', '0.0.0.0'),
  port: env.int('PORT', 1337),
  url: env('PUBLIC_URL', 'https://api.example.com'),
  proxy: {
    koa: true,
    maxIpsCount: 1,
  },
  app: {
    keys: env.array('APP_KEYS'),
  },
});
```

| Option | 中文说明 |
|---|---|
| `proxy.koa` | 设为 `true` 后信任 forwarded headers |
| `proxy.maxIpsCount` | Strapi 5.52+；从 forwarded chain 尾部读取多少个 proxy 地址。单层 proxy 通常设为 1 |
| `proxy.ipHeader` | Strapi 5.52+；client IP 来源 header，默认 `X-Forwarded-For`，Cloudflare 等场景可改为其他 header |

**Original:** Leaving `maxIpsCount` at 0 means unlimited.

**中文译文:** `maxIpsCount: 0` 表示无限制，会增加 client 伪造 forwarded chain 的风险。应按真实 proxy 层数设置。
