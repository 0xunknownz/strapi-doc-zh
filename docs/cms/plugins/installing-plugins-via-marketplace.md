# 📖 对照翻译：Using the Marketplace

> Source: `docusaurus/docs/cms/plugins/installing-plugins-via-marketplace.md`  
> Upstream SHA: `f6544ec3c91dde3b61798851d3e34200f59e83e0`

**Original:** The in-app Marketplace lists plugins and providers with badges, search, filters, and links to detailed Community Hub pages.

**中文译文:** Strapi admin panel 内置 **Marketplace**，用于发现 plugin 与 provider。它提供搜索、筛选、排序、维护状态 badge，并可跳转到 Strapi Community Hub 查看安装与版本兼容信息。

**Original:** Strapi includes built-in plugins such as Documentation, GraphQL, and Sentry.

**中文译文:** Strapi 自带 Documentation、GraphQL、Sentry 等官方 plugins；Marketplace 则用于寻找更多 community plugins 和 providers。

## Marketplace vs Community Hub

**Original:** The in-app Marketplace can list plugins for multiple Strapi major versions; v4 and v5 plugins are not cross-compatible, while providers can be compatible with both.

**中文译文:** Admin panel 中可能显示面向不同 Strapi major version 的 plugin。**Strapi v4 plugin 与 v5 plugin 不兼容**，安装前应在 Community Hub 中确认支持版本。Provider 的兼容范围通常更宽，可同时支持 v4 / v5 plugin。

## Plugin/provider cards

**Original:** Cards show name, Strapi-maintained or verified badges, GitHub stars/download counts, description, and a More link.

**中文译文:** 每张卡片通常包含：
- 名称；
- Strapi-maintained logo 或 verified badge；
- GitHub stars / download count；
- Description；
- **More**：跳转 Community Hub 查看具体 Strapi version、安装说明与项目链接。

## Installing

**Original:** Open Marketplace, choose Plugins or Providers, open More, then follow the integration-specific instructions.

**中文译文:** 安装流程：
1. 在 admin panel 打开 **Marketplace**；
2. 选择 **Plugins** 或 **Providers** tab；
3. 找到目标项目并点击 **More**；
4. 在 Community Hub 页面确认版本要求；
5. 按该 plugin/provider 自己的 installation / configuration 指南操作。

**Original:** If no existing plugin fits your use case, you can create your own.

**中文译文:** 如果 Marketplace 没有满足需求的 plugin，可以使用 [Plugin SDK](/cms/plugins-development/create-a-plugin) 开发自己的 Strapi plugin。
