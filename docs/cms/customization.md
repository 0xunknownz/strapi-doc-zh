# 📖 对照翻译：Customization

> Source: `docusaurus/docs/cms/customization.md`  
> Upstream SHA: `da828aec6a5cf184e1285ced2c18d9b29a0d5ae5`

**Original:** Strapi contains a backend server and admin panel, both of which can be customized to extend routes, policies, middlewares, themes, and more.

**中文译文:** Strapi 主要包含 back-end server 与 admin panel 两部分，两者都提供 customization 能力。Server 可以扩展 routes、policies、middlewares、controllers、services、models；Admin panel 则可以定制 logos、theme、translations、menu 等。

## Back end

**Original:** The backend server receives requests, interacts with data created through Content-Type Builder and Content Manager, and returns responses.

**中文译文:** Back-end server 负责：
- 接收 HTTP request；
- 根据 Content-Type Builder 定义的 schema 处理数据；
- 访问 Content Manager 保存的内容；
- 通过 REST / GraphQL 或自定义 route 返回 response。

**Original:** Most backend server parts can be customized.

**中文译文:** Back-end customization 主要包括 routes、policies、middlewares、controllers、services、models、request/response 处理与 webhooks。详见 [Backend customization](/cms/backend-customization)。

## Admin panel

**Original:** The admin panel is the graphical UI used to define content structures, manage content, and interact with built-in or third-party plugins.

**中文译文:** Admin panel 是编辑人员使用的 GUI，用于定义 content structure、管理 entries、使用内置 / third-party plugins。其 branding、theme、translation 与 extension points 都可以自定义。

**Original:** Database customization and external front-end customization are outside this section.

**中文译文:** 本章节不直接覆盖：
- Database engine 本身的 customization；
- 消费 Strapi Content API 的外部 front-end application。

Database 相关请参阅 installation / database configuration；前端集成请参阅 Strapi integrations。
