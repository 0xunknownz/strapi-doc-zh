# 📖 对照翻译：Proxying Strapi with HAProxy

> Source: `docusaurus/docs/cms/deployment/guides/haproxy.md`  
> Upstream SHA: `8fd0ce997994eb14d702049a4e1efc668d7dcb6e`

**Original:** Configure Strapi's public URL/proxy settings, then terminate TLS and health-check Strapi with HAProxy.

**中文译文:** HAProxy 场景先配置 Strapi public URL 与 proxy trust，再由 HAProxy frontend terminate TLS，backend 使用 `/_health` 做 health check，并可进一步做 load balancing。

## Prerequisites

**中文译文:** 需要 Strapi 5、HAProxy 2.2+、public domain、TLS PEM（certificate + private key 合并）、sudo access。

## Strapi proxy settings

**Original:** HAProxy adds `X-Forwarded-For`; `X-Forwarded-Proto` must be set explicitly.

**中文译文:** `option forwardfor` 会写入 client IP；但 HTTPS protocol 需要显式设置：

`http-request set-header X-Forwarded-Proto https if { ssl_fc }`

Strapi 用该 header 判断 refresh-token cookie 是否应标记 `Secure`。

## Minimal configuration

```text
defaults
    mode http
    option forwardfor
    timeout connect 5s
    timeout client 60s
    timeout server 60s

frontend strapi_front
    bind :80
    bind :443 ssl crt /etc/haproxy/certs/api.example.com.pem
    http-request redirect scheme https unless { ssl_fc }
    http-request set-header X-Forwarded-Proto https if { ssl_fc }
    default_backend strapi_back

backend strapi_back
    option httpchk
    http-check send meth GET uri /_health
    http-check expect status 204
    server strapi1 127.0.0.1:1337 check
```

**中文译文:** 关键点：
- `bind :443 ssl crt` 读取单一 PEM；
- `option forwardfor` 传递 client IP；
- Health check 明确使用 `GET /_health` 并要求 `204`；
- Upload 较大时还要提高 `timeout client/server`。

## Validate and reload

```bash
sudo haproxy -c -f /etc/haproxy/haproxy.cfg
sudo systemctl reload haproxy
```

## Docker

**中文译文:** 容器内 backend 应使用 `server strapi1 strapi:1337 check`，不能用 loopback。Strapi 同样需要 bind `0.0.0.0`。

## Multiple instances

```text
backend strapi_back
    balance roundrobin
    option httpchk
    http-check send meth GET uri /_health
    http-check expect status 204

    server strapi1 10.0.0.11:1337 check
    server strapi2 10.0.0.12:1337 check
```

**中文译文:** HAProxy 很适合多 Strapi instance，但要同时遵守 [multi-instance caveats](../../../snippets/multi-instance-strapi-caveats.md)，尤其 schema migration 与 cron。

## Troubleshooting

**中文译文:** 常见问题：
- `503 Service Unavailable`：没有 backend 通过 health check；
- Health check 失败：确认实际返回严格为 204；
- Upload timeout：提高 Strapi file limit 与 HAProxy timeouts；
- Client IP 错误：检查 `option forwardfor` 与 `proxy.koa`；
- Cookie 没有 `Secure`：检查 `X-Forwarded-Proto`；
- Reset link 指向 localhost：检查 `server.url`。
