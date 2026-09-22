# 📖 对照翻译：Deployment guides

> Source: `docusaurus/docs/cms/deployment/guides.md`  
> Upstream SHA: `badf245cedf14c7910b8cbe69943e0b219651e2e`

**Original:** These guides cover reverse proxies and process managers for production Strapi deployment.

**中文译文:** Deployment guides 主要覆盖 production 中常见的 reverse proxy、TLS termination 与 process manager 配置。

**Original:** Prerequisite: have a Strapi project and read general deployment guidelines.

**中文译文:** 前置条件：
- 已创建 Strapi project；
- 已阅读 [general deployment guidelines](/cms/deployment#general-guidelines)。

## Available guides

**Original:** Proxying with Caddy.

**中文译文:** [Caddy](/cms/deployment/guides/caddy)：使用 Caddy reverse proxy，并利用其 automatic HTTPS。

**Original:** Proxying with HAProxy.

**中文译文:** [HAProxy](/cms/deployment/guides/haproxy)：通过 HAProxy load balancer 暴露 Strapi HTTPS。

**Original:** Proxying with Nginx.

**中文译文:** [Nginx](/cms/deployment/guides/nginx)：最常见的 Strapi reverse proxy / HTTPS setup。

**Original:** Proxying with Traefik.

**中文译文:** [Traefik](/cms/deployment/guides/traefik)：适合 containerized Strapi deployment 与 dynamic routing。

**Original:** Using PM2.

**中文译文:** [PM2](/cms/deployment/guides/pm2)：让 Strapi process 持续运行，并支持 server reboot 后自动启动。

**Original:** For third-party hosting platforms and general production requirements, see the main deployment page.

**中文译文:** 第三方 hosting platform 与 production 基础要求请继续参考 [Deployment](/cms/deployment) 主文档。
