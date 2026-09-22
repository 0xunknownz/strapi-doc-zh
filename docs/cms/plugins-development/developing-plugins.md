# 📖 对照翻译：Developing Strapi plugins

> Source: `docusaurus/docs/cms/plugins-development/developing-plugins.md`  
> Upstream SHA: `b5eb48164478c393294fa25f304a60ad25df2c56`

**Original:** Strapi plugins extend core functionality using Admin Panel API, Server API, or MCP server tools. Plugins can be local or published.

**中文译文:** Strapi plugin 可以扩展 admin panel、back-end server 与 MCP server。开发完成后可以：
- 作为 local plugin 只服务一个项目；
- 发布 npm；
- 提交 Strapi Marketplace 与社区共享。

## Recommended path

**Original:** Create a plugin with Plugin SDK, understand its structure, use plugin APIs, then follow advanced guides.

**中文译文:** 推荐学习路径：
1. 使用 [Plugin SDK](/cms/plugins-development/create-a-plugin) 创建 plugin；
2. 熟悉 [plugin structure](/cms/plugins-development/plugin-structure)；
3. 根据需求使用 Admin Panel API / Server API / MCP extension API；
4. 继续阅读 use-case guides。

**Original:** Use a different major version for Strapi 5 plugins versus v4-compatible releases.

**中文译文:** 如果同一个 plugin 同时维护 Strapi v4 / v5 版本，建议为 v5-compatible release 使用不同 major version，避免用户错误安装。

## Plugin APIs

**Original:** Admin Panel API lets plugins extend the admin panel.

**中文译文:** **Admin Panel API**：添加 navigation / settings、React UI、injection zones、Redux state、Content Manager extension 等。

**Original:** Server API lets plugins extend the backend.

**中文译文:** **Server API**：添加 content-types、routes、controllers、services、policies、middlewares、config、lifecycle 等。

**Original:** MCP extension APIs let plugins register custom tools.

**中文译文:** **MCP extension API**：通过 `strapi.ai.mcp` 注册 custom MCP tools，使 AI client 可以触发 plugin-specific action。

**Original:** Plugins can also register custom fields.

**中文译文:** Plugin 还可以注册 [custom fields](/cms/features/custom-fields)。

## Guides

**中文译文:** 官方 guides 包括：
- Plugin 中存储 / 访问数据；
- 从 server 向 admin panel 传数据；
- 为 plugin 创建 admin permissions；
- 为 plugin 创建 reusable components。
