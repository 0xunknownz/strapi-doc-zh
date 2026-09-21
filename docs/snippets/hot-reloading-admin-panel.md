# 📖 对照翻译：Admin panel hot reloading

> Source: `docusaurus/docs/snippets/hot-reloading-admin-panel.md`  
> Upstream SHA: `e94ebcd3248f716826ddc44d58c8bb6fe39a4c76`

**Original:** In Strapi 5, the server runs in `watch-admin` mode by default, so the admin panel auto-reloads whenever you change its code.

**中文译文:** Strapi 5 development server 默认启用 `watch-admin`，修改 admin panel code 后会自动 reload，这简化了 admin customization 与 front-end plugin development。

**Original:** Disable it with `yarn develop --no-watch-admin`.

**中文译文:** 如需关闭 admin watcher，可运行 `yarn develop --no-watch-admin`（npm 项目使用对应 CLI alias）。
