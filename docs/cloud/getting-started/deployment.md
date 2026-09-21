# 📖 对照翻译：Project deployment with the Cloud dashboard

> Source: `docusaurus/docs/cloud/getting-started/deployment.md`  
> Upstream SHA: `419f2227d718333fec58817eac1bf4a232c17855`

**Original:** Project deployment with the Cloud dashboard

**中文译文:** 使用 Cloud dashboard 部署项目

**Original:** Deploy your Strapi project on Strapi Cloud using the dashboard by choosing a plan, connecting a Git repository, configuring your project settings, and setting up billing details.

**中文译文:** 通过 Cloud dashboard 将 Strapi 项目部署到 Strapi Cloud：选择方案、连接 Git repository、配置项目设置，并填写计费信息。

**Original:** This is a step-by-step guide for deploying your project on Strapi Cloud for the first time, using the Cloud dashboard.

**中文译文:** 本指南将分步骤介绍如何首次使用 Cloud dashboard 将项目部署到 Strapi Cloud。

## Prerequisites

**Original:** Before you can deploy your Strapi application on Strapi Cloud using the Cloud dashboard, you need to have the following prerequisites:

- Strapi version `4.8.2` or higher.
- Project database must be compatible with PostgreSQL. Strapi does not support and does not recommend using any external databases, though it's possible to configure one.
- Project source code hosted on GitHub or GitLab. The connected repository can contain multiple Strapi applications. Each Strapi app must be in a separate directory.
- Specifically for GitLab: at least have Maintainer permissions for the project to import on Strapi Cloud.

**中文译文:** 在使用 Cloud dashboard 将 Strapi 应用部署到 Strapi Cloud 之前，需要满足以下条件：

- Strapi 版本为 `4.8.2` 或更高版本。
- 项目数据库必须兼容 PostgreSQL。Strapi 不支持且不建议使用外部数据库，不过仍可以进行配置，详见 [advanced database configuration](/cloud/advanced/database)。
- 项目源代码托管在 GitHub 或 GitLab。一个已连接的 repository 可以包含多个 Strapi 应用，但每个 Strapi app 必须位于独立目录中。
- 如果使用 GitLab，需要对要导入 Strapi Cloud 的项目至少拥有 **Maintainer** 权限。

## Logging in to Strapi Cloud

**Original:** 1. Navigate to the Strapi Cloud login page.

**中文译文:** 1. 打开 [Strapi Cloud](https://cloud.strapi.io) 登录页面。

**Original:** 2. You have the options to log in with GitHub, Google, GitLab or via One Time Password. Choose your preferred option and log in. This initial login will create your Strapi Cloud account. Once logged in, you will be redirected to the Strapi Cloud Projects page where you can create your first Strapi Cloud project.

**中文译文:** 2. 可以选择使用 **GitHub**、**Google**、**GitLab** 或 **One Time Password** 登录。选择合适的方式完成登录。首次登录时会自动创建 Strapi Cloud 账户；登录成功后，你会进入 Strapi Cloud 的 *Projects* 页面，并可以从这里创建第一个 Strapi Cloud 项目。

## Creating a project

**Original:** 1. From the Projects page, click the Create project button.

**中文译文:** 1. 在 *Projects* 页面点击 **Create project**。

**Original:** 2. You will be redirected to the project creation interface. This interface contains 3 steps: choosing a plan, connecting a remote git repository, and setting up the project.

**中文译文:** 2. 页面会跳转到项目创建界面。创建流程包含 3 个步骤：选择方案、连接远程 Git repository，以及配置项目。

**Original:** 3. Choose a plan and a billing period for your Strapi Cloud project.

**中文译文:** 3. 为 Strapi Cloud 项目选择方案和 billing period。价格详情请参阅 [Pricing](https://strapi.io/pricing-cloud)。

**Original:** 4. Connect a git repository to your new Strapi Cloud project. You may first have to select a git provider. If you have already deployed a project with one git provider, you can afterward deploy another project using another provider by clicking on the Switch git provider button and selecting either GitHub or GitLab.

**中文译文:** 4. 为新的 Strapi Cloud 项目连接 Git repository。你可能需要先选择 Git provider。如果之前已经使用某个 provider 部署过项目，后续仍可以点击 **Switch git provider**，在 GitHub 与 GitLab 之间切换，并通过另一个 provider 部署其他项目。

**Original:** Choose your path for your new Strapi Cloud project! Select one of the tabs below depending on how you wish to proceed:

- by deploying a prebuilt Strapi template (recommended for new users and beginners — only available on GitHub),
- or by deploying your existing Strapi project.

**中文译文:** 为新的 Strapi Cloud 项目选择创建方式：

- 部署预构建的 Strapi template（推荐新用户和初学者使用，仅 GitHub 支持）；
- 或部署已经存在的 Strapi 项目。

### Prebuilt Strapi template

**Original:** 4.a. After connecting your GitHub account, click on the Use template button.

**中文译文:** 4.a. 连接 GitHub 账户后，点击 **Use template**。

**Original:** 4.b. In the Create repository with template modal, choose the GitHub account where the repository will be created.

**中文译文:** 4.b. 在 *Create repository with template* 弹窗中，选择要在哪个 GitHub 账户下创建 repository。

**Original:** 4.c. Click on the Create repository button. A modal will confirm the creation of the repository.

**中文译文:** 4.c. 点击 **Create repository**。随后弹窗会确认 repository 已创建。

**Original:** 4.d. If you have already given Strapi Cloud access to all repositories of your GitHub account, go directly to the next step. If not, you will be redirected to a GitHub modal where you will have to allow Strapi Cloud access to the newly created repository.

**中文译文:** 4.d. 如果已经授权 Strapi Cloud 访问 GitHub 账户中的全部 repositories，可以直接进入下一步。否则，系统会跳转到 GitHub 授权界面，你需要允许 Strapi Cloud 访问刚创建的 repository。更多信息请参阅 [GitHub documentation](https://docs.github.com/en/apps/overview)。

**Original:** 4.e. Back in the project creation interface, the Account and Repository fields now match the newly created template.

**中文译文:** 4.e. 返回项目创建界面后，*Account* 和 *Repository* 字段会自动对应刚创建的 template repository。

### Existing Strapi project

**Original:** Connect the GitHub or GitLab account that owns the repository you want to deploy. This can be different from the account you used to log into your Strapi Cloud account.

**中文译文:** 请连接实际拥有目标 repository 的 GitHub 或 GitLab 账户。这个账户可以与登录 Strapi Cloud 时使用的账户不同。

**Original:** 4.a. If you have already given Strapi Cloud access to all repositories of your GitHub or GitLab account, go directly to the next step. If not, you will be redirected to a modal where you will have to allow Strapi Cloud permission to access some or all your repositories on GitHub/GitLab.

**中文译文:** 4.a. 如果已经授权 Strapi Cloud 访问 GitHub 或 GitLab 账户中的全部 repositories，可以直接进入下一步。否则，系统会跳转到授权界面，你需要允许 Strapi Cloud 访问部分或全部 repositories。更多信息请参阅 GitHub 和 GitLab 的相关授权文档。

**Original:** 4.c. Back in the project creation interface, select the Account and the Repository you want to deploy.

**中文译文:** 4.c. 返回项目创建界面，选择希望部署的 *Account* 和 *Repository*。

## Setting up your Strapi Cloud project

**Original:** 5. Set up your Strapi Cloud project.

**中文译文:** 5. 配置 Strapi Cloud 项目。

**Original:** 5.a. Fill in the following information:

| Setting name | Instructions |
|---|---|
| Display name | The name is automatically populated based on the repository you selected, but you can edit it if needed. |
| Git branch | Choose from the drop-down the branch you want to deploy. |
| Deploy on push | Tick this box to automatically trigger a deployment when changes are pushed to your selected branch. When disabled, you will need to manually deploy the latest changes. |
| Region | Choose the geographic location of the servers where your Strapi application is hosted. Selected region can either be US (East), Europe (West) or Asia (Southeast). |

**中文译文:** 5.a. 填写以下信息：

| 设置项 | 说明 |
|---|---|
| Display name | 系统会根据所选 repository 自动填写名称，你也可以根据需要修改。 |
| Git branch | 从下拉菜单中选择要部署的 branch。 |
| Deploy on push | 勾选后，只要选定 branch 有新变更被 push，就会自动触发 deployment。关闭后，需要手动部署最新变更。 |
| Region | 选择托管 Strapi 应用的服务器地理区域。可选 US (East)、Europe (West) 或 Asia (Southeast)。 |

**Original:** The Git branch and "Deploy on push" settings can be modified afterwards through the project settings. However, the hosting region can only be chosen during the creation of the project.

**中文译文:** *Git branch* 和 **Deploy on push** 后续都可以在项目设置中修改；但 hosting region 只能在项目创建阶段选择，创建后无法直接更改。详见 [Project Settings](/cloud/projects/settings)。

### Advanced settings

**Original:** 5.b. (optional) Click on Show advanced settings to fill in the following options:

| Setting name | Instructions |
|---|---|
| Base directory | Write the name of the directory where your Strapi app is located in the repository. This is useful if you have multiple Strapi apps in the same repository or if you have a monorepo. |
| Environment variables | Click on Add variable to add environment variables used to configure your Strapi app. You can also add environment variables by adding a `.env` file to the root of your Strapi app directory. The environment variables defined in the `.env` file will be used by Strapi Cloud. |
| Node version | Choose a Node version from the drop-down. The default Node version will automatically be chosen to best match the version of your Strapi project. If you manually choose a version that doesn't match with your Strapi project, the build will fail but the explanation will be displayed in the build logs. |

**中文译文:** 5.b. （可选）点击 **Show advanced settings**，配置以下高级选项：

| 设置项 | 说明 |
|---|---|
| Base directory | 填写 Strapi app 在 repository 中所在的目录名称。如果一个 repository 中包含多个 Strapi app，或项目采用 monorepo，这项设置尤其有用。 |
| Environment variables | 点击 **Add variable** 添加用于配置 Strapi app 的环境变量。也可以在 Strapi app 根目录添加 `.env` 文件，Strapi Cloud 会使用该文件中定义的环境变量。更多信息请参阅 [Environment variables](/cms/configurations/environment/)。 |
| Node version | 从下拉菜单中选择 Node 版本。默认情况下，系统会自动选择最匹配当前 Strapi 项目的 Node 版本。如果手动选择的版本与项目不兼容，build 会失败，具体原因会显示在 build logs 中。 |

**Original:** You can use environment variable to connect your project to an external database rather than the default one used by Strapi Cloud. If you would like to revert and use Strapi's default database again, remove your `DATABASE_` environment variables (no automatic migration implied).

**中文译文:** 可以使用 environment variable 将项目连接到外部数据库，而不是使用 Strapi Cloud 默认数据库，具体可参阅 [database configuration](/cms/configurations/database#environment-variables-in-database-configurations)。如果之后希望恢复使用 Strapi 默认数据库，请删除对应的 `DATABASE_` 环境变量；这一操作**不会**自动迁移已有数据。

**Original:** You can also set up here a custom email provider. Sendgrid is set as the default one for the Strapi applications hosted on Strapi Cloud.

**中文译文:** 还可以在这里配置自定义 email provider。托管在 Strapi Cloud 上的 Strapi 应用默认使用 SendGrid，详情请参阅 [providers configuration](/cms/features/email#providers)。

## Setting up billing details

**Original:** 1. Click on the Continue to billing button. You will be redirected to the billing page where you can enter your payment details and review your invoice.

**中文译文:** 1. 点击 **Continue to billing**。系统会跳转到 billing 页面，你可以在这里填写付款信息并核对 invoice。

**Original:** 2. In the Payment method section, add a credit card. This card will be used for all project-related transactions, including add-ons and overages.

**中文译文:** 2. 在 *Payment method* 中添加信用卡。该卡会用于所有与项目有关的交易，包括 add-ons 和 overages。

**Original:** 3. In the Billing information section, fill in your payment details and billing address.

**中文译文:** 3. 在 *Billing information* 中填写付款信息与 billing address。

**Original:** 4. Review the Invoice section. When purchasing a monthly subscription, the subscription price will be prorated for the remaining days in the current billing cycle. Optionally, expand the Discount code section to enter a code.

**中文译文:** 4. 核对 *Invoice*。购买月度订阅时，本期订阅费用会根据当前 billing cycle 剩余天数按比例计算。若有优惠码，可展开 *Discount code* 输入。

**Original:** Taxes may be added to your invoice based on your billing address:

- In the EU, UK, Canada, and India, providing a valid VAT ID exempts you from VAT. If no valid VAT ID is provided, VAT will be added to your invoice.
- In the US, applicable sales taxes are calculated based on your state and address.

**中文译文:** 发票可能会根据 billing address 加收税费：

- 在欧盟、英国、加拿大和印度，提供有效 VAT ID 可以免除 VAT；如果未提供有效 VAT ID，则发票中会加入 VAT。
- 在美国，适用的 sales tax 会根据所在州和地址计算。

**Original:** 5. Click on the Subscribe button to finalize the creation of your new Strapi Cloud project.

**中文译文:** 5. 点击 **Subscribe**，完成新 Strapi Cloud 项目的创建。

## Deploying your project

**Original:** After confirming the project creation, you will be redirected to your Project dashboard where you will be able to follow its creation and first deployment.

**中文译文:** 确认创建项目后，系统会跳转到 *Project dashboard*。你可以在这里跟踪项目创建过程以及首次 deployment 的进度。

**Original:** While your project is deploying, you can already start configuring some of your project settings.

**中文译文:** 项目正在部署时，你已经可以开始配置部分 [project settings](/cloud/projects/settings)。

**Original:** If an error occurs during the project creation, the progress indicator will stop and display an error message. You will see a Retry button next to the failed step, allowing you to restart the creation process.

**中文译文:** 如果项目创建过程中发生错误，进度指示器会停止，并显示错误信息。失败步骤旁会出现 **Retry** 按钮，可用它重新启动创建流程。

**Original:** Once your project is successfully deployed, the creation tracker will be replaced by your deployments list and you will be able to visit your Cloud hosted project. Don't forget to create the first Admin user before sharing your Strapi project.

**中文译文:** 项目部署成功后，创建进度跟踪器会被 deployments 列表取代，你也可以直接访问托管在 Cloud 上的项目。在将 Strapi 项目分享给其他人之前，别忘了先创建第一个 Admin user。

## What to do next?

**Original:** Now that you have deployed your project via the Cloud dashboard, we encourage you to explore the following ideas to have an even more complete Strapi Cloud experience:

- Invite other users to collaborate on your project.
- Check out the deployments management documentation to learn how to trigger new deployments for your project.

**中文译文:** 现在你已经通过 Cloud dashboard 完成项目部署，可以继续探索以下内容，以获得更完整的 Strapi Cloud 使用体验：

- 邀请其他用户 [collaborate on your project](/cloud/projects/collaboration)。
- 阅读 [deployments management 文档](/cloud/projects/deploys)，了解如何为项目触发新的 deployment。
