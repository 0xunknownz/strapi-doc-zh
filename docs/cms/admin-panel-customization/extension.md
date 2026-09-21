# 📖 对照翻译：Admin panel extension

> Source: `docusaurus/docs/cms/admin-panel-customization/extension.md`  
> Upstream SHA: `dd2fac64a5ba2fd851e5ac79e73bf80a465e2528`

**Original:** Strapi's React-based admin panel can be extended locally via `/src/admin/app` for project-specific needs or through plugins for reusable, distributable extensions across multiple Strapi instances.

**中文译文:** Strapi admin panel 基于 React，可以采用两种扩展方式：
- 通过 `/src/admin/app` 做当前项目专用的 local extension；
- 通过 plugin 开发可复用、可分发到多个 Strapi instances 的 extension。

**Original:** Extending the admin panel means leveraging React to adapt and enhance UI/features, including custom components or new field types.

**中文译文:** 扩展 admin panel 本质上是利用其 React foundation 改造界面和功能，例如添加 custom component、navigation、setting section，或引入新 field type。

| Approach | Scope | Entry point | 中文说明 |
|---|---|---|---|
| Local extension | One project | `/src/admin/app.(js|ts)` + `/src/admin/extensions/` | 适合单个 Strapi instance 的定制 |
| Plugin extension | Any project installing plugin | `[plugin-name]/admin/src/index.(js|ts)` | 适合复用、版本化和分发 |

**Original:** Plugin developers can use Admin Panel API to add links/settings, inject React components, manage Redux state, and extend Content Manager views.

**中文译文:** Plugin developer 可使用 [Admin Panel API](/cms/plugins-development/admin-panel-api)：
- 添加 navigation link / settings section；
- 向预定义区域 inject React component；
- 通过 Redux 管理 state；
- 扩展 Content Manager Edit / List views 等。

**Original:** Project-specific customization can directly update `/src/admin/app`, which may import files from `/src/admin/extensions`.

**中文译文:** 只针对一个项目时，推荐直接修改 `/src/admin/app.js|ts`，并把自定义 module / asset 放到 `/src/admin/extensions` 后 import。

**Original:** Server-side behavior for a core plugin is not changed under `/src/admin`; use `./src/extensions/<plugin-name>/strapi-server.js|ts`.

**中文译文:** `/src/admin` 只负责 admin bundle。若要改变 core plugin 的 **server behavior**，例如 Upload plugin API，应使用 `./src/extensions/<plugin-name>/strapi-server.js|ts`，参阅 [Plugins extension](/cms/plugins-development/plugins-extension)。

## When to consider a plugin

**Original:** Start with direct customization for project-specific needs. Move to a plugin when customization is duplicated, distributed/versioned, requires independent tests, or shared ownership.

**中文译文:** 项目专用需求优先直接改 `/src/admin/app`。出现以下情况时应考虑迁移到 plugin：
- 多个 Strapi 项目重复同一 customization；
- 需要独立 version / distribution（内部或 Marketplace）；
- 需要脱离单个 project codebase 的 automated testing；
- 多团队需要共同维护与 release management。

**Original:** For replacing the rich text editor see the dedicated page; for plugin integration start with Admin Panel API.

**中文译文:** 替换默认 Rich text editor 请参阅 [WYSIWYG editor customization](/cms/admin-panel-customization/wysiwyg-editor)；开发可复用 admin plugin 建议从 [Admin Panel API](/cms/plugins-development/admin-panel-api) 开始。
