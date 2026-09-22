# 📖 对照翻译：Proxying Strapi with Nginx

> Source: `docusaurus/docs/cms/deployment/guides/nginx.md`  
> Upstream SHA: `aa0770d21092a73a8d7a81e39c2a70a81cf0c13f`

**Original:** Configure Strapi public URL/proxy settings, then add an Nginx server block forwarding the original host, IP, protocol, and WebSocket upgrade headers.

**中文译文:** Nginx reverse proxy 需要两部分：Strapi 自身配置 public URL / proxy trust，以及 Nginx `server` block 转发 Host、client IP、protocol 与 WebSocket upgrade headers。

## Basic Nginx server block

```nginx title="/etc/nginx/sites-available/strapi.conf"
map $http_upgrade $connection_upgrade {
    default upgrade;
    ''      close;
}

server {
    listen 80;
    server_name api.example.com;

    client_max_body_size 100M;

    location / {
        proxy_pass http://127.0.0.1:1337;
        proxy_http_version 1.1;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
    }
}
```

**中文译文:** `Upgrade` / `Connection` 对 remote data transfer 的 WebSocket connection 很重要；`X-Forwarded-Proto` 让 Strapi 知道原始 request 是否为 HTTPS。

## Enable and validate

```bash
sudo ln -s /etc/nginx/sites-available/strapi.conf /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

**中文译文:** RHEL 系 distribution 通常使用 `/etc/nginx/conf.d/`，无需 Debian/Ubuntu 的 symlink 结构。

## Docker

**Original:** Use the Docker service name.

```nginx
proxy_pass http://strapi:1337;
```

**中文译文:** Nginx container 中的 `127.0.0.1` 指向 Nginx 自己，因此需使用 shared network 上的 Strapi service name。Strapi 必须 bind `0.0.0.0`。

**Original:** Use `expose` rather than publishing Strapi's port publicly.

**中文译文:** 推荐只 publish Nginx 80/443，对 Strapi 使用 Docker `expose: 1337`，让请求只能经 proxy 到达。

## TLS termination

**Original:** Nginx needs an external certificate issuer such as Certbot, acme.sh, lego, container companions, or an upstream load balancer/CDN.

**中文译文:** Nginx 本身不会自动申请 certificate，可配合：
- Certbot；
- acme.sh；
- lego；
- nginx-proxy/acme-companion；
- Cloud load balancer / CDN。

**Original code (kept unchanged):**

```nginx
server {
    listen 80;
    server_name api.example.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    http2 on;
    server_name api.example.com;

    ssl_certificate     /etc/nginx/certs/fullchain.pem;
    ssl_certificate_key /etc/nginx/certs/privkey.pem;

    client_max_body_size 100M;

    location / {
        proxy_pass http://127.0.0.1:1337;
        proxy_http_version 1.1;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
    }
}
```

**中文译文:** Nginx 1.25.1+ 使用独立 `http2 on;`；旧版本可写 `listen 443 ssl http2;`。

## Upload limits

**中文译文:** `client_max_body_size`、Strapi `formidable.maxFileSize` 与 provider `sizeLimit` 都要允许目标 file size，否则最小值会先拒绝 request。

## Troubleshooting

**中文译文:**
- `502 Bad Gateway`：Nginx 无法连接 Strapi；
- `413 Request Entity Too Large`：提高 Nginx + Strapi + provider limits；
- Client IP 变 `127.0.0.1`：启用 `proxy.koa`；
- Reset URL 为 localhost：设置 `server.url` 并 rebuild；
- Refresh cookie 缺少 `Secure`：确保转发 `X-Forwarded-Proto`。
