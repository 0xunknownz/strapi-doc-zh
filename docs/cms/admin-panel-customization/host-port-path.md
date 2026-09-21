# 📖 对照翻译：Admin panel Host, port, and path configuration

> Source: `docusaurus/docs/cms/admin-panel-customization/host-port-path.md`  
> Upstream SHA: `94afa1bbdae99f3bb74ae7dd32e65e1b7b574239`

**Original:** Configure the Strapi admin panel's host, port, and URL path in `config/admin.[ts|js]` to change where it is accessible from its default location at `/admin`.

**中文译文:** 可以在 `config/admin.js|ts` 中修改 admin panel 的 host、port 与 URL path，使其不再使用默认的 `http://localhost:1337/admin`。

## Update path only

**Original:** By default, backend and admin share `http://localhost:1337/`; admin is under `/admin`, Content API under `/api`.

**中文译文:** 默认情况下，Strapi back end 与 admin panel 共用 host / port：`http://localhost:1337/`。Admin panel 使用 `/admin` path，而 Content API 默认使用 `/api` prefix。

**Original:** To move admin to `/dashboard`, set `url`.

```js title="/config/admin.js"
module.exports = ({ env }) => ({
  url: "/dashboard",
});
```

**中文译文:** 例如把 admin path 改为 `/dashboard`，只需设置 `admin.url`。

**Original:** If host/port in server config remain defaults, changing only admin config is enough.

**中文译文:** 如果没有拆分 admin / API server，并且 `/config/server.js|ts` 中 host / port 保持正常配置，则只修改 admin `url` 即可。

```js title="/config/server.js"
module.exports = ({ env }) => ({
  host: env("HOST", "0.0.0.0"),
  port: env.int("PORT", 1337),
});
```

## Update host and port

**Original:** If admin and backend run on different servers, set admin `host` and `port`.

**中文译文:** 如果 admin panel 与 back-end server 分开部署，需要在 admin configuration 中显式设置 admin 的 `host` / `port`。

```js title="./config/admin.js"
module.exports = ({ env }) => ({
  host: "my-host.com",
  port: 3000,
  // url: '/dashboard'
});
```

**Original:** Behind a reverse proxy, ensure forwarded headers are correct and explicitly configure the public admin origin when different from API origin.

**中文译文:** 在 reverse proxy 后部署时，应正确转发 `X-Forwarded-*` 等 headers。如果 admin 与 API 使用不同 public origin（domain / host / port），建议显式配置 admin origin。

**Original:** Since Strapi 5.51, changing admin `url` also requires matching `auth.cookie.path`.

**中文译文:** **Strapi 5.51+ 重要变更：** 修改 admin `url` 时，还必须让 `auth.cookie.path` 与新 path 一致，否则 login request 虽然成功，但 admin panel 无法读取 authentication cookie，之后的 request 会被拒绝并重新跳回 login page。

```js title="/config/admin.js"
module.exports = ({ env }) => ({
  url: "/dashboard",
  auth: {
    cookie: {
      path: "/dashboard",
    },
  },
});
```

**中文译文:** `auth.cookie.path` 会被 inline 到 admin bundle，因此修改后需要重新 build admin panel。
