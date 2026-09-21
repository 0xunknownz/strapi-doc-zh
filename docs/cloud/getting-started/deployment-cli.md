# 📖 对照翻译：Project deployment with the Command Line Interface (CLI)

> Source: `docusaurus/docs/cloud/getting-started/deployment-cli.md`  
> Upstream SHA: `e62b0f1a2560ca056495eec02916119b0e569ce7`

**Original:** Project deployment with the Command Line Interface (CLI)

**中文译文:** 使用 Command Line Interface（CLI）部署项目

**Original:** Deploy a Strapi project to Strapi Cloud using the `strapi login`, `strapi link`, and `strapi deploy` CLI commands, with optional automatic deployment on git repository commits.

**中文译文:** 使用 `strapi login`、`strapi link` 和 `strapi deploy` CLI 命令将 Strapi 项目部署到 Strapi Cloud；也可以选择在 Git repository 有新 commit 时自动触发部署。

**Original:** This is a step-by-step guide for deploying your project on Strapi Cloud using the Command Line Interface.

**中文译文:** 本指南将分步骤介绍如何通过 Command Line Interface 将项目部署到 Strapi Cloud。

## Prerequisites

**Original:** Before you can deploy your Strapi application on Strapi Cloud using the Command Line Interface, you need to have the following prerequisites:

- Have a Google, GitHub or GitLab account.
- Have an already created Strapi Cloud project.
- Have an already created Strapi project, stored locally. The project must be less than 100MB.
- Have available storage in your hard drive where the temporary folder of your operating system is stored.

**中文译文:** 在通过 Command Line Interface 将 Strapi 应用部署到 Strapi Cloud 之前，需要满足以下条件：

- 拥有 Google、GitHub 或 GitLab 账户。
- 已经创建 Strapi Cloud 项目，可参阅 [Project deployment with the Cloud dashboard](/cloud/getting-started/deployment)。
- 已经创建并保存在本地的 Strapi 项目，可参阅 CMS 文档中的 [Installing from CLI](/cms/installation/cli)。项目大小必须小于 100MB。
- 操作系统临时目录所在磁盘需要有足够的可用空间。

## Logging in to Strapi Cloud

**Original:** 1. Open your terminal.

**中文译文:** 1. 打开终端。

**Original:** 2. Navigate to the folder of your Strapi project, stored locally on your computer.

**中文译文:** 2. 进入本地保存 Strapi 项目的目录。

**Original:** 3. Enter the following command to log into Strapi Cloud:

**中文译文:** 3. 运行以下命令登录 Strapi Cloud：

**Original code (kept unchanged):**

```bash
# Yarn
yarn strapi login

# NPM
npx run strapi login
```

**中文译文:** 根据项目使用的包管理器执行对应命令。命令保持原样。

**Original:** 4. In the browser window that opens automatically, confirm that the code displayed is the same as the one written in the terminal message.

**中文译文:** 4. 浏览器会自动打开新窗口。确认页面显示的代码与终端消息中的代码一致。

**Original:** 5. Still in the browser window, choose whether to login via Google, GitHub or GitLab. The window should confirm the successful login soon after.

**中文译文:** 5. 继续在浏览器窗口中选择使用 Google、GitHub 或 GitLab 登录。完成后，页面会提示登录成功。

## Linking your local project to Strapi Cloud

**Original:** From your terminal, still from the folder of your Strapi project, enter the following command to link the local project to your existing Strapi Cloud project:

**中文译文:** 在终端中保持位于 Strapi 项目目录，然后运行以下命令，将本地项目关联到已有的 Strapi Cloud 项目：

**Original code (kept unchanged):**

```bash
# Yarn
yarn strapi link

# NPM
npx run strapi link
```

**中文译文:** 根据包管理器执行对应的 `link` 命令。命令保持原样。

**Original:** Select the Strapi Cloud project you want to link from the list displayed in the terminal.

**中文译文:** 在终端显示的项目列表中，选择希望关联的 Strapi Cloud 项目。

## Deploying your project

**Original:** From your terminal, still from the folder of your Strapi project, enter the following command to deploy the project:

**中文译文:** 在终端中保持位于 Strapi 项目目录，然后运行以下命令部署项目：

**Original code (kept unchanged):**

```bash
# Yarn
yarn strapi deploy

# NPM
npx run strapi deploy
```

**中文译文:** 根据包管理器执行对应的 `deploy` 命令。命令保持原样。

**Original:** Follow the progression bar in the terminal until confirmation that the project was successfully deployed with Strapi Cloud.

**中文译文:** 观察终端中的进度条，直到看到项目已成功部署到 Strapi Cloud 的确认信息。

### Automatically deploying subsequent changes

**Original:** By default, when deploying a project with the Cloud CLI, you need to manually deploy again all subsequent changes by running the corresponding `deploy` command everytime you make a change.

**中文译文:** 默认情况下，通过 Cloud CLI 部署项目后，每次产生新的变更，都需要再次运行对应的 `deploy` 命令手动部署。

**Original:** Another option is to enable automatic deployment through a git repository. To do so:

1. Host your code on a git repository, such as GitHub or GitLab.
2. Connect your Strapi Cloud project to the repository.
3. In Projects Settings > General, tick the box for the "Deploy the project on every commit pushed to this branch" setting. From now on, a new deployment to Strapi Cloud will be triggered any time a commit is pushed to the connected git repository.

**中文译文:** 另一种方式是通过 Git repository 启用自动部署。操作步骤如下：

1. 将代码托管到 Git repository，例如 GitHub 或 GitLab。
2. 将 Strapi Cloud 项目连接到该 repository，具体可参阅 [Projects Settings > General](/cloud/projects/settings#general) 中的 *Connected repository* 设置。
3. 仍然在 *Projects Settings > General* 中，勾选 **Deploy the project on every commit pushed to this branch**。之后，只要有 commit 被推送到已连接的 Git repository，就会自动触发一次新的 Strapi Cloud 部署。

**Original:** Automatic deployment is compatible with all other deployment methods, so once a git repository is connected, you can trigger a new deployment to Strapi Cloud from the Cloud dashboard, from the CLI, or by pushing new commits to your connected repository.

**中文译文:** 自动部署可以与其他部署方式同时使用。因此，一旦连接 Git repository，你既可以从 [Cloud dashboard](/cloud/projects/deploys) 触发部署，也可以通过 [CLI](/cloud/cli/cloud-cli#strapi-deploy) 部署，还可以通过向已连接的 repository 推送新 commit 来触发部署。

## What to do next?

**Original:** Now that you have deployed your project via the Command Line Interface, we encourage you to explore the following ideas to have an even more complete Strapi Cloud experience:

- Visit the Cloud dashboard to follow insightful metrics and information on your Strapi project.
- Check out the full Command Line Interface documentation to learn about the other commands available.

**中文译文:** 现在你已经通过 Command Line Interface 完成项目部署，可以继续探索以下内容，以获得更完整的 Strapi Cloud 使用体验：

- 前往 Cloud dashboard，查看 Strapi 项目的 [关键指标和信息](/cloud/projects/overview)。
- 阅读完整的 [Command Line Interface 文档](/cloud/cli/cloud-cli)，了解其他可用命令。
