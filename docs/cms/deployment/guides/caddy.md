# 📖 对照翻译：Proxying Strapi with Caddy

> Source: `docusaurus/docs/cms/deployment/guides/caddy.md`  
> Upstream SHA: `f0c02948e4be1404942ab66ab5fa1f5109e6a634`

**Original:** Point `server.url` at your public domain, trust proxy headers, then use a minimal Caddyfile. Caddy automatically obtains and renews TLS certificates.

**中文译文:** 使用 Caddy 时，先让 Strapi 知道 public URL 并信任 forwarded headers，然后通过很短的 Caddyfile 反向代理到 Strapi。Caddy 会自动申请、续期 TLS certificate。

## Prerequisites

**Original:** Strapi 5 app, Caddy, public DNS A record, ports 80/443, and shell access.

**中文译文:** 前置条件：
- 可正常运行的 Strapi 5 application；
- Caddy；
- Domain 的 DNS `A` record 指向 server；
- Public 80 / 443 ports；
- Shell / sudo access。

## Strapi configuration

**Original:** Set `server.url` and `server.proxy`.

**中文译文:** 先应用共用的 [public URL](../../../snippets/proxy-server-url.md) 与 [proxy trust](../../../snippets/proxy-trust-headers.md) 配置。修改 `/config/server.js` 后需要重新 build admin panel。

**Original:** Caddy writes its own forwarded headers and discards client-provided `X-Forwarded-*` values by default.

**中文译文:** Caddy 默认会丢弃 client 自带的 `X-Forwarded-*` 并写入自己的 headers，因此单层 Caddy 场景通常比直接信任任意 forwarded chain 更安全。若前面还有 CDN / load balancer，应在 Caddy 配置 trusted proxies，并同步增加 Strapi `maxIpsCount`。

## Caddyfile

```text
api.example.com {
    reverse_proxy 127.0.0.1:1337
}
```

**中文译文:** Public domain 出现在 site block 后，Caddy 会自动：
- 获取 Let's Encrypt certificate；
- HTTP → HTTPS redirect；
- 自动续期；
- 设置 `X-Forwarded-For` / `X-Forwarded-Proto` / `X-Forwarded-Host`；
- 支持 WebSocket proxy。

## Validate and reload

```bash
sudo caddy validate --config /etc/caddy/Caddyfile
sudo systemctl reload caddy
```

**中文译文:** Reload 前先 validate，避免错误配置直接导致站点中断。

## Request-body cap

```text
api.example.com {
    request_body {
        max_size 100MB
    }

    reverse_proxy 127.0.0.1:1337
}
```

**中文译文:** Caddy 默认不限制 request body。若显式设置 `max_size`，它应不小于 Strapi `formidable.maxFileSize`。

## Docker

**Original:** In containers, proxy to the Strapi service name, not `127.0.0.1`.

**中文译文:** Caddy 与 Strapi 同在 Docker network 时：

```text
api.example.com {
    reverse_proxy strapi:1337
}
```

Strapi 必须 bind `0.0.0.0`，否则其他 container 无法连接。

**Original:** Persist Caddy's `/data` directory.

**中文译文:** 必须为 Caddy `/data` 挂载 persistent volume，因为 certificate state 存在这里；否则每次 container restart 都会重新申请证书并可能触发 Let's Encrypt rate limit。

## Verify

```bash
curl -I https://api.example.com/_health
```

**中文译文:** 正常应返回 HTTP `204` 与 `strapi: You are so French!` header。之后再确认 admin HTTPS 登录、Media Library URL、真实 client IP。

## Troubleshooting

**Original:** Common issues include certificate failures, 502, upload limits, proxy IP, and localhost links.

**中文译文:** 常见故障：
- Certificate 失败：检查 DNS 与 80 port；
- `502 Bad Gateway`：检查 Strapi process / port / bind address；
- Upload 太大：同时提高 Caddy 与 Strapi limits；
- Strapi 只看到 `127.0.0.1`：检查 `proxy.koa`；
- Reset email 指向 localhost：检查 `server.url` 并 rebuild admin。
