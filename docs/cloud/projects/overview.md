# 📖 对照翻译：Cloud projects overview

> Source: `docusaurus/docs/cloud/projects/overview.md`  
> Upstream SHA: `f23df2cba7cfedc3059d03262ce8ddd93c130916`

**Original:** Cloud projects overview

**中文译文:** Cloud 项目概览

**Original:** Projects page lists all apps with status and quick actions; selecting one opens a dashboard with metrics and controls.

**中文译文:** *Projects* 页面会列出全部应用及其状态和快捷操作；选择某个项目后，会打开包含指标与管理操作的 dashboard。

**Original:** The *Projects* page displays a list of all your Strapi Cloud projects. From here you can manage your projects and access the corresponding applications.

**中文译文:** *Projects* 页面会显示你所有 Strapi Cloud 项目的列表。你可以在这里管理项目，并访问对应的应用。

**Original:** Each project card displays the following information:

- the project name
- the last successful deployment’s date of the Production environment
- the current status of the project:
  - *Disconnected*, if the project repository is not connected to Strapi Cloud
  - *Suspended*, if the project has been suspended
  - *Incompatible version*, if the project is using a Strapi version that is not compatible with Strapi Cloud

**中文译文:** 每张项目卡片都会显示以下信息：

- 项目名称；
- Production environment 最近一次成功 deployment 的日期；
- 项目当前状态：
  - *Disconnected*：项目 repository 尚未连接到 Strapi Cloud；
  - *Suspended*：项目已被暂停，可参阅 [Project suspension](/cloud/getting-started/usage-billing#project-suspension) 了解如何恢复；
  - *Incompatible version*：项目使用的 Strapi 版本与 Strapi Cloud 不兼容。

**Original:** Each project card also displays a menu icon to access the following options:

- **Visit App**: to be redirected to the application
- **Go to Deployments**: to be redirected to the *Deployment* page
- **Go to Settings**: to be redirected to the *Settings* page

**中文译文:** 每张项目卡片还会显示菜单按钮，可使用以下操作：

- **Visit App**：跳转到应用；
- **Go to Deployments**：进入 [*Deployment*](/cloud/projects/deploys) 页面；
- **Go to Settings**：进入 [*Settings*](/cloud/projects/settings) 页面。

**Original:** Click on the Product updates button in the navigation bar to check out the latest features and fixes released.

**中文译文:** 点击导航栏中的 *Product updates* 按钮，可以查看最新发布的功能与修复。

## Accessing a project's dashboard

**Original:** From the *Projects* page, click on any project card to access its dashboard. It displays the project and environment details and gives access to the deployment history, logs, observability and all available settings.

**中文译文:** 在 *Projects* 页面点击任意项目卡片即可进入对应 dashboard。这里会展示项目与 environment 详情，并提供 deployment history、logs、observability 以及全部可用设置的入口。

**Original:** From the dashboard header of a chosen project, you can:

- switch or add an environment,
- use the **Share** button to invite users to collaborate on the project and see the icons of those who have already been invited,
- use the **Settings** button to access the settings of the project and its existing environments,
- navigate between deployments, logs and observability,
- trigger a new deployment and visit your application.

**中文译文:** 在所选项目 dashboard 的 header 中，你可以：

- 切换或添加 environment；
- 使用 **Share** 邀请其他用户参与项目协作，并查看已经受邀用户的头像，详见 [Collaboration](/cloud/projects/collaboration)；
- 使用 **Settings** 访问项目及现有 environments 的设置；
- 在 deployments、logs 和 observability 页面之间切换；
- 触发新的 deployment，并访问应用。

**Original:** Your project dashboard also displays:

- the list of all the deployments of your environment,
- the project and environment details in a box on the right of the interface, including:
  - a summary of API, bandwidth, and storage consumption,
  - the name of the branch and a **Manage** button to be redirect to the branch settings,
  - the name of the base directory,
  - the Strapi version number,
  - the Strapi app's url.

**中文译文:** 项目 dashboard 还会显示：

- 当前 environment 的全部 deployment 列表，详见 [Deployments history](/cloud/projects/deploys-history)；
- 界面右侧的项目与 environment 详情，包括：
  - API、bandwidth 和 storage 用量摘要，完整明细请参阅 [Project observability](/cloud/projects/observability)；
  - branch 名称，以及用于进入 branch 设置的 **Manage** 按钮；
  - base directory 名称；
  - Strapi 版本号；
  - Strapi app 的 URL。
