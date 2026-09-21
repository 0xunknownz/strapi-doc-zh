# 📖 对照翻译：Command Line Interface (CLI)

> Source: `docusaurus/docs/cloud/cli/cloud-cli.md`  
> Upstream SHA: `22c876603bcbb4885e9e8456f5afa16bb24567e8`

**Original:** Command Line Interface (CLI)

**中文译文:** Command Line Interface（CLI）

**Original:** CLI commands handle login, project linking, deploying, listing, and logout without needing a remote repository.

**中文译文:** CLI 命令可以完成登录、项目关联、部署、项目列表查询和退出登录，并且不要求项目必须托管在远程 repository。

**Original:** Strapi Cloud comes with a Command Line Interface (CLI) which allows you to log in and out, link a local project to an existing Strapi Cloud project, and deploy it without having to host it on a remote git repository. The CLI works with both the `yarn` and `npm` package managers.

**中文译文:** Strapi Cloud 提供 Command Line Interface（CLI），可以用于登录和退出、把本地项目关联到已有 Strapi Cloud 项目，并在无需远程 Git repository 的情况下进行部署。CLI 同时支持 `yarn` 和 `npm` package manager。

**Original:** It is recommended to install Strapi locally only, which requires prefixing all of the following `strapi` commands with the package manager used for the project setup (e.g `npm run strapi help` or `yarn strapi help`) or a dedicated node package executor (e.g. `npx strapi help`).

**中文译文:** 建议只在项目本地安装 Strapi。因此，下面所有 `strapi` 命令通常都需要加上项目使用的 package manager 前缀，例如 `npm run strapi help` 或 `yarn strapi help`；也可以使用专门的 Node package executor，例如 `npx strapi help`。

## `strapi login`

**Original:** Alias: `strapi cloud:login`

**中文译文:** 别名：`strapi cloud:login`

**Original:** Log in Strapi Cloud.

**中文译文:** 登录 Strapi Cloud。

```bash
strapi login
```

**Original:** This command automatically opens a browser window to first ask you to confirm that the codes displayed in both the browser window and the terminal are the same. Then you will be able to log into Strapi Cloud via Google, GitHub or GitLab. Once the browser window confirms successful login, it can be safely closed.

**中文译文:** 该命令会自动打开浏览器窗口。首先确认浏览器和终端显示的代码一致，然后即可通过 Google、GitHub 或 GitLab 登录 Strapi Cloud。浏览器提示登录成功后，可以安全关闭该窗口。

**Original:** If the browser window doesn't automatically open, the terminal will display a clickable link as well as the code to enter manually.

**中文译文:** 如果浏览器没有自动打开，终端也会显示可点击链接以及需要手动输入的代码。

## `strapi link`

**Original:** Alias: `strapi cloud:link`

**中文译文:** 别名：`strapi cloud:link`

**Original:** Links project in the current folder to an existing project in Strapi Cloud.

**中文译文:** 将当前目录中的项目关联到已有 Strapi Cloud 项目。

```bash
strapi link
```

**Original:** This command connects your local project in the current directory with an existing project on your Strapi Cloud account. You will be prompted to select the project you wish to link from a list of available projects hosted on Strapi Cloud.

**中文译文:** 该命令会把当前目录中的本地项目连接到 Strapi Cloud 账户中的已有项目。终端会显示可用项目列表，并提示你选择要关联的目标项目。

## `strapi deploy`

**Original:** Alias: `strapi cloud:deploy`

**中文译文:** 别名：`strapi cloud:deploy`

**Original:** Deploy a linked local project (< 100MB) to Strapi Cloud.

**中文译文:** 将已经关联的本地项目（小于 100MB）部署到 Strapi Cloud。

```bash
strapi deploy
```

**Original:** This command must be used after the `login` and `link` commands. It deploys a local Strapi project to an existing Strapi Cloud project that is linked to the current folder. The terminal will inform you when the project is successfully deployed on Strapi Cloud.

**中文译文:** 该命令必须在 `login` 和 `link` 之后使用。它会把本地 Strapi 项目部署到与当前目录关联的已有 Strapi Cloud 项目。部署成功后，终端会显示确认信息。

**Original:** Once the project is first linked and deployed on Strapi Cloud with the CLI, the `deploy` command can be reused to trigger a new deployment of the same project.

**中文译文:** 项目第一次通过 CLI 完成关联和部署后，后续可以继续使用 `deploy` 为同一项目触发新的 deployment。

**Original:** Once you deployed your project, if you visit the Strapi Cloud dashboard, you may see some limitations as well as impacts due to creating a Strapi Cloud project that is not in a remote repository and which was deployed with the CLI.

- Some areas in the dashboard that are usually reserved to display information about the git provider will be blank.
- Some buttons, such as the **Trigger deploy** button, will be greyed out and unclickable since, unless you have connected a git repository to your Strapi Cloud project.

**中文译文:** 如果 Strapi Cloud 项目没有连接远程 repository，而是直接通过 CLI 部署，那么进入 Cloud dashboard 后会看到一些限制：

- Dashboard 中通常用于显示 Git provider 信息的部分区域会为空；
- 某些按钮（例如 **Trigger deploy**）会变灰且无法点击，除非之后为 Strapi Cloud 项目 [连接 Git repository](/cloud/getting-started/deployment-cli#automatically-deploying-subsequent-changes)。

## `strapi projects`

**Original:** Alias: `strapi cloud:projects`

**中文译文:** 别名：`strapi cloud:projects`

**Original:** Lists all Strapi Cloud projects associated with your account.

**中文译文:** 列出当前账户关联的全部 Strapi Cloud 项目。

```bash
strapi projects
```

**Original:** This command retrieves and displays a list of all projects hosted on your Strapi Cloud account.

**中文译文:** 该命令会获取并显示 Strapi Cloud 账户下托管的全部项目。

## `strapi logout`

**Original:** Alias: `strapi cloud:logout`

**中文译文:** 别名：`strapi cloud:logout`

**Original:** Log out of Strapi Cloud.

**中文译文:** 退出 Strapi Cloud。

```bash
strapi logout
```

**Original:** This command logs you out of Strapi Cloud. Once the `logout` command is run, a browser page will open and the terminal will display a confirmation message that you were successfully logged out. You will not be able to use the `deploy` command anymore.

**中文译文:** 该命令会退出 Strapi Cloud。运行 `logout` 后会打开浏览器页面，同时终端显示退出成功的确认信息。退出后将无法继续使用 `deploy` 命令，直到再次登录。
