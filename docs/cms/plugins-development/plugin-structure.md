# 📖 对照翻译：Plugin structure

> Source: `docusaurus/docs/cms/plugins-development/plugin-structure.md`  
> Upstream SHA: `8b7042fd59eba72adec1d74f7b79fac5474dd09c`

**Original:** A Strapi plugin is divided into an `admin/` part and a `server/` part.

**中文译文:** Plugin SDK 生成的 Strapi plugin 分成两个独立部分：

| Part | Folder | 中文说明 | API |
|---|---|---|---|
| Admin panel | `admin/` | React UI、navigation、settings、translation、injection 等 | Admin Panel API |
| Backend server | `server/` | Content-types、routes、controllers、services、middlewares 等 | Server API |

## Server-only plugins

**Original:** A plugin can contain only the server part when no admin UI is needed.

**中文译文:** 如果 plugin 只扩展 API / server logic，可以完全不提供 admin UI。Server-only plugin 仍可拥有自己的 content-types、controller actions、routes 等。

## Admin plugin vs project customization

**Original:** Project-specific admin customization can be done under `/src/admin` without creating a plugin.

**中文译文:** 如果 UI customization 只服务一个项目，也可以直接在 `/src/admin` 扩展 admin panel；当代码需要复用、独立 version / publish / ownership 时，再选择 plugin。

## Next steps

**中文译文:** 继续阅读：
- [Admin Panel API](/cms/plugins-development/admin-panel-api)
- [Server API](/cms/plugins-development/server-api)
- [Plugin development guides](/cms/plugins-development/developing-plugins#guides)
