# 📖 对照翻译：Backend customization examples cookbook

> Source: `docusaurus/docs/cms/backend-customization/examples.md`  
> Upstream SHA: `94b5d6d98b6db9f20bbd8bece5eae68481d4b2d7`

**Original:** A cookbook of real-world backend customization examples using the FoodAdvisor demo application, demonstrating custom routes, controllers, services, policies, and middlewares.

**中文译文:** 本 examples cookbook 基于 Strapi 官方 FoodAdvisor demo，通过真实场景演示 custom routes、controllers、services、policies 与 middlewares 的组合方式。

**Original:** This section is intended for developers seeking deeper understanding of Strapi backend customization.

**中文译文:** 本章节面向希望深入理解 Strapi back-end customization 的开发者，重点不是单独解释 API，而是展示多个 server elements 如何在真实项目中配合。

**Original:** Examples extend FoodAdvisor, the official Strapi demo: a Strapi backend in `/api` and a Next.js frontend in `/client`.

**中文译文:** 示例围绕官方 [FoodAdvisor](https://github.com/strapi/foodadvisor) 展开：
- `/api`：Strapi back end；
- `/client`：Next.js front end。

**Original:** Prerequisites include understanding Strapi as a headless CMS, reading the backend customization introduction, and optionally running FoodAdvisor locally.

**中文译文:** 建议前置条件：
- 已了解 Strapi 是 headless CMS，能使用 Content-Type Builder / Content Manager；
- 已阅读 [Backend customization 总览](/cms/backend-customization)；
- 若要实际运行示例，clone FoodAdvisor 并启动 back end 与 front end。默认 admin panel 为 `http://localhost:1337/admin`，front end 为 `http://localhost:3000`。

**Original:** Cookbook topics include authentication, controllers/services, policies/errors, routes, and global middlewares.

**中文译文:** Cookbook 主要主题：
- [JWT authentication flow](/cms/backend-customization/examples/authentication)；
- [Custom controllers and services](/cms/backend-customization/examples/services-and-controllers)；
- [Custom policies and custom errors](/cms/backend-customization/examples/policies)；
- [Custom routes](/cms/backend-customization/examples/routes)；
- [Custom global middlewares](/cms/backend-customization/examples/middlewares)。
