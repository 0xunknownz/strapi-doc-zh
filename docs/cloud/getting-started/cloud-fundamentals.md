# 📖 对照翻译：Strapi Cloud fundamentals

> Source: `docusaurus/docs/cloud/getting-started/cloud-fundamentals.md`  
> Upstream SHA: `62f69aafe9ed6a10dd2474a67f88a780b9c6334c`

**Original:** Strapi Cloud fundamentals

**中文译文:** Strapi Cloud 基础概念

**Original:** Strapi Cloud is a PaaS hosting platform for deploying Strapi CMS projects, offering three pricing plans with different features and support levels, two user roles (owners and maintainers), and REST/GraphQL APIs that behave identically to self-hosted servers.

**中文译文:** Strapi Cloud 是一个用于部署 Strapi CMS 项目的 PaaS 托管平台。它提供 3 种具有不同功能与支持级别的定价方案、2 种用户角色（owners 和 maintainers），其 REST/GraphQL API 的行为与自托管服务器完全一致。

**Original:** Before going any further into this Strapi Cloud documentation, we recommend you to acknowledge the main concepts below. They will help you to understand how Strapi Cloud works, and ensure a smooth Strapi Cloud experience.

**中文译文:** 在继续阅读 Strapi Cloud 文档之前，建议先了解下面这些核心概念。它们有助于你理解 Strapi Cloud 的工作方式，并获得更顺畅的使用体验。

**Original:** **Hosting Platform** — Strapi Cloud is a hosting platform that allows you to deploy already existing Strapi projects created with Strapi CMS (Content Management System). Strapi Cloud is *not* the SaaS (Software-as-a-Service) version of Strapi CMS and should rather be considered as a PaaS (Platform-as-a-Service). Feel free to refer to the CMS documentation to learn more about Strapi CMS.

**中文译文:** **Hosting Platform（托管平台）** —— Strapi Cloud 是一个托管平台，用于部署已经使用 Strapi CMS（Content Management System）创建好的 Strapi 项目。Strapi Cloud **不是** Strapi CMS 的 SaaS（Software-as-a-Service）版本，更准确地说，它应被视为 PaaS（Platform-as-a-Service）。如需进一步了解 Strapi CMS，请参阅 [CMS 文档](https://docs.strapi.io/cms/intro)。

**Original:** **Strapi Cloud Pricing Plans** — As a Strapi Cloud user you have the choice between 3 plans: Starter, Pro, and Business. Depending on the plan, you have access to different functionalities, support and customization options. In this Strapi Cloud documentation, the Pro and Business badges can be displayed below a section's title to indicate that the feature is only available starting from the corresponding plan. If no badge is shown, the feature is available on the Starter plan. Only Pro and Business badges are used in Cloud docs because Starter is the baseline plan; the Starter badge component exists for consistency with other Strapi documentation but is not displayed on Cloud pages.

**中文译文:** **Strapi Cloud Pricing Plans** —— Strapi Cloud 提供 3 种方案：Starter、Pro 和 Business。不同方案可使用的功能、支持级别和自定义选项有所不同，详细信息请参阅 [Pricing 页面](https://strapi.io/pricing-cloud)。在 Strapi Cloud 文档中，章节标题下方可能会显示 Pro 或 Business 徽标，用于说明该功能从对应方案起才可用。如果没有显示徽标，则表示 Starter 方案也可以使用该功能。Cloud 文档仅使用 Pro 和 Business 徽标，因为 Starter 是基准方案；Starter 徽标组件虽然为了与其他 Strapi 文档保持一致而存在，但不会显示在 Cloud 页面中。

**Original:** **Types of Strapi Cloud users** — There can be 2 types of users on a Strapi Cloud project: owners and maintainers. The owner is the one who has created the project and has therefore access to all features and options for the project. Maintainers are users who have been invited to contribute to an already created project by its owner. Maintainers, as documented in the Collaboration page, cannot view and access all features and options from the Strapi Cloud dashboard.

**中文译文:** **Strapi Cloud 用户类型** —— 一个 Strapi Cloud 项目中可以有 2 类用户：owners 和 maintainers。owner 是项目创建者，因此可以访问该项目的所有功能与选项。maintainers 则是由 owner 邀请、参与现有项目协作的用户。正如 [Collaboration](/cloud/projects/collaboration) 页面所述，maintainers 无法在 Strapi Cloud dashboard 中查看和访问全部功能与选项。

**Original:** **Support** — The level of support provided by the Strapi Support team depends on the Strapi Cloud plan you subscribed for. The Starter and Pro plans include Basic support while the Business plan includes Standard support. Please refer to the dedicated support article for all details regarding support levels.

**中文译文:** **Support** —— Strapi Support 团队提供的支持级别取决于你订阅的 Strapi Cloud 方案。Starter 和 Pro 方案包含 Basic support，Business 方案则包含 Standard support。关于各支持级别的完整说明，请参阅 [专门的支持文章](https://support.strapi.io/support/solutions/articles/67000680833-what-is-supported-by-the-strapi-team#Not-Supported)。

**Original:** **API access in Strapi Cloud vs self-hosted** — The REST and GraphQL APIs behave the same on Strapi Cloud and on self-hosted servers. The only differences are the URLs:

**中文译文:** **Strapi Cloud 与自托管环境中的 API 访问** —— REST 和 GraphQL API 在 Strapi Cloud 与自托管服务器上的行为完全相同，唯一的区别在于 URL：

**Original:** Base API domain: On Strapi Cloud, your API uses the domain of the environment (e.g. `https://<project>.strapiapp.com/api/...`), or your custom domain if you set one. A self-hosted project would use whatever domain you expose.

**中文译文:** Base API domain：在 Strapi Cloud 中，API 使用当前环境的域名，例如 `https://<project>.strapiapp.com/api/...`；如果配置了自定义域名，也可以使用自定义域名。自托管项目则使用你实际对外暴露的域名。自定义域名相关信息请参阅 [Domains 文档](/cloud/projects/settings#domains)。

**Original:** Media Library URLs: Media fields in REST and GraphQL responses from Strapi Cloud always use the project media domain (e.g. `<project>.media.strapiapp.com`), even when you access the API through a custom domain. Self-hosted projects return URLs from the configured upload provider, so the domain can match your own site or CDN. When you move a project from self-hosted to Strapi Cloud, make sure your frontend reads the absolute URLs returned by the API or accepts the Strapi Cloud media domain.

**中文译文:** Media Library URL：Strapi Cloud 的 REST 和 GraphQL 响应中，媒体字段始终使用项目的媒体域名，例如 `<project>.media.strapiapp.com`；即使你通过自定义域名访问 API，也仍然如此。自托管项目返回的 URL 由所配置的 upload provider 决定，因此域名可能与你自己的网站或 CDN 一致。将项目从自托管环境迁移到 Strapi Cloud 时，请确保前端直接使用 API 返回的绝对 URL，或者允许访问 Strapi Cloud 的媒体域名。
