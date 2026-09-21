# 📖 对照翻译：Different types of middlewares

> Source: `docusaurus/docs/snippets/middleware-types.md`  
> Upstream SHA: `98133a7b84cf598371853baac8e0b4ebe5139068`

**Original:** In Strapi, 3 middleware concepts coexist.

**中文译文:** Strapi 中存在 3 类不同 middleware 概念，需要区分它们的 scope 与 registration 方式。

**Original:** Global middlewares are configured/enabled for the entire Strapi server application. They can be application-level or API-level. Plugins can also add global middlewares.

**中文译文:** **Global middlewares**：通过 middleware configuration 为整个 Strapi server 启用。自定义文件可以位于 application level 或 API level；plugin 也可以注册 global middleware。

**Original:** Route middlewares have a more limited scope and are configured at route level.

**中文译文:** **Route middlewares**：scope 更窄，只绑定到特定 route，在 router configuration 中声明。

**Original:** Document Service middlewares apply to Document Service API and have their own implementation/lifecycle behavior.

**中文译文:** **Document Service middlewares**：作用于 Document Service API 调用链，registration 与 lifecycle 独立于 HTTP route middleware。参阅 [Document Service middlewares](/cms/api/document-service/middlewares)。
