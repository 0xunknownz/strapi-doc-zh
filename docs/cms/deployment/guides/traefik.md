# 📖 对照翻译：Proxying Strapi with Traefik

> Source: `docusaurus/docs/cms/deployment/guides/traefik.md`  
> Upstream SHA: `692349cebcf34db84309a5be2cd7f0d325e41f0d`

**Original:** Configure Strapi public URL/proxy settings, then use Docker labels so Traefik discovers the Strapi container, routes to port 1337, and obtains TLS certificates.

**中文译文:** Traefik 特别适合 containerized Strapi：static config 定义 entry points / certificate resolver，dynamic routing 则通过 Strapi container labels 自动发现。

## Static configuration

```yml title="./traefik/traefik.yml"
entryPoints:
  web:
    address: ':80'
    http:
      redirections:
        entryPoint:
          to: websecure
          scheme: https
          permanent: true
  websecure:
    address: ':443'

providers:
  docker:
    exposedByDefault: false

certificatesResolvers:
  letsencrypt:
    acme:
      email: admin@example.com
      storage: /acme/acme.json
      tlsChallenge: {}
```

**中文译文:** `exposedByDefault: false` 很重要，避免 Traefik 自动公开 Docker host 上所有 containers。

## Docker labels

```yml
strapi:
  image: my-strapi-app
  environment:
    HOST: 0.0.0.0
    PORT: 1337
    PUBLIC_URL: https://api.example.com
  labels:
    - 'traefik.enable=true'
    - 'traefik.http.routers.strapi.rule=Host(`api.example.com`)'
    - 'traefik.http.routers.strapi.entrypoints=websecure'
    - 'traefik.http.routers.strapi.tls.certresolver=letsencrypt'
    - 'traefik.http.services.strapi.loadbalancer.server.port=1337'
```

**中文译文:** 最容易遗漏的是 `loadbalancer.server.port=1337`。Strapi container 不需要公开 host port，只需与 Traefik 共享 Docker network。

**Original:** Persist ACME storage.

**中文译文:** `/acme/acme.json` 必须放在 persistent volume，否则每次 restart 都重新申请 certificate，可能触发 Let's Encrypt rate limit。

**Original:** Docker socket access is effectively root-equivalent.

**中文译文:** 将 `/var/run/docker.sock` 挂给 Traefik 意味着非常高的主机权限。`:ro` 只限制 socket file 本身，并不真正限制 Docker API 能力。Production 应谨慎保护 Traefik dashboard，并考虑 socket proxy。

## Forwarded headers

**Original:** Traefik sets and sanitizes forwarded headers by default.

**中文译文:** Traefik 默认会生成 `X-Forwarded-For` / `X-Forwarded-Proto` 等。如果前面还有 CDN / LB，应配置 `forwardedHeaders.trustedIPs`，并让 Strapi `maxIpsCount` 覆盖完整 proxy chain。

## Request-size cap

```yml
- 'traefik.http.middlewares.strapi-limit.buffering.maxRequestBodyBytes=104857600'
- 'traefik.http.routers.strapi.middlewares=strapi-limit'
```

**中文译文:** Traefik buffering middleware 可以返回 `413` 拦截超大 request，但它会先读完整 request body，并可能 spill to disk。大型 Media Library upload 场景通常更适合让 Strapi `formidable.maxFileSize` 控制。

## Troubleshooting

**中文译文:**
- `404 page not found`：router rule / label / network 不匹配；
- `502 Bad Gateway`：port label 错误或 Strapi 未 bind `0.0.0.0`；
- 无 certificate：检查 DNS 与 443 reachability；
- 每次 restart 重新签证书：ACME storage 未持久化；
- Upload `413`：提高或删除 buffering limit；
- Client IP 为 Traefik container：启用 Strapi `proxy.koa`。
