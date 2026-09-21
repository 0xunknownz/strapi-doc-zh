# 📖 对照翻译：Installing from CLI

> Source: `docusaurus/docs/cms/installation/cli.md`  
> Upstream SHA: `842fab2e40b1ed2b113564550870b5db52812b86`

**Original:** The Strapi CLI is the fastest way to install Strapi locally using `npx create-strapi@latest`, with options to configure TypeScript, databases (`--dbclient`, `--dbhost`, etc.), and other setup preferences via command-line flags.

**中文译文:** Strapi CLI 是在本地安装 Strapi 最快捷的方式。可以使用 `npx create-strapi@latest` 创建项目，并通过 command-line flags 配置 TypeScript、database（例如 `--dbclient`、`--dbhost`）以及其他初始化选项。

**Original:** Strapi CLI (Command Line Interface) installation scripts are the fastest way to get Strapi running locally. The following guide is the installation option most recommended by Strapi.

**中文译文:** Strapi CLI（Command Line Interface）安装脚本是让 Strapi 在本地运行起来的最快方式，也是 Strapi 官方最推荐的安装方式。

## Preparing the installation

**Original:** Before installing Strapi, make sure the installation prerequisites are satisfied. A supported database is also required for any Strapi project.

**中文译文:** 安装 Strapi 之前，请先满足 [installation prerequisites](../../snippets/installation-prerequisites.md)。任何 Strapi 项目还必须使用受支持的 database，具体版本参见 [Supported databases](../../snippets/supported-databases.md)。

## Creating a Strapi project

**Original:** Follow the steps below to create a new Strapi project, being sure to use the appropriate command for your installed package manager.

**中文译文:** 按照以下步骤创建新的 Strapi 项目，并根据本机使用的 package manager 选择对应命令。

**Original:** In a terminal, run the following command:

```bash
npx create-strapi@latest
```

**中文译文:** 在 terminal 中运行：

```bash
npx create-strapi@latest
```

**Original:**
- `npx` runs a command from a npm package
- `create-strapi` is the Strapi package
- `@latest` indicates that the latest version of Strapi is used

**中文译文:**
- `npx`：执行 npm package 中提供的 command；
- `create-strapi`：Strapi 的 package；
- `@latest`：指定使用最新版本的 Strapi。

**Original:** The older `npx create-strapi-app@latest` command still works and will provide the exact same experience as the newer `npx create-strapi@latest` command.

**中文译文:** 旧命令 `npx create-strapi-app@latest` 仍然可用，使用体验与新的 `npx create-strapi@latest` 完全一致。

**Original:** Instead of npx, the traditional npm command can be used too, with `npm create strapi@latest`.

Please note the additional dash between create and strapi when using npx: `npx create-strapi` vs. `npm create strapi`.

**中文译文:** 除了 npx，也可以使用传统 npm 命令 `npm create strapi@latest`。

请特别注意两种写法的差异：npx 使用 `npx create-strapi`，`create` 与 `strapi` 之间有连字符；npm 则使用 `npm create strapi`。

**Original:** With pnpm, run:

```bash
pnpm create strapi
```

On Strapi Cloud, the pnpm version is managed by Corepack: the version pinned in your project's `package.json` `packageManager` field is honored automatically, or Corepack's bundled default is used if none is pinned.

**中文译文:** 使用 pnpm 时运行：

```bash
pnpm create strapi
```

在 Strapi Cloud 中，pnpm 版本由 Corepack 管理：如果项目的 `package.json` 中通过 `packageManager` 字段锁定了版本，会自动使用该版本；否则使用 Corepack 自带的默认版本。

**Original:** The terminal will ask you whether you want to `Login/Signup` or `Skip` this step. Use arrow keys and press `Enter` to make your choice. If you choose to login, you'll receive a 30-day trial of the Growth plan that will be automatically applied to your created project. If you skip this step, the project will fall back to the CMS Free plan.

**中文译文:** Terminal 会询问是执行 `Login/Signup` 还是 `Skip`。使用方向键选择并按 `Enter` 确认。如果选择登录，新创建的项目会自动获得 30 天 Growth plan trial；如果跳过，则项目使用 CMS Free plan。

**Original:** The terminal will ask you a few questions. For each of them, if you press `Enter` instead of typing something, the default answer (Yes) will be used.

**中文译文:** Terminal 接下来会询问若干初始化问题。对于每个问题，如果直接按 `Enter` 而不输入内容，将使用默认答案（Yes）。

**Original:** You can skip these questions using various options passed to the installation command. Please refer to the CLI installation options table for the full list of available options.

**中文译文:** 可以通过向安装 command 传递不同 options 跳过这些交互问题。完整可用选项参见下方 CLI installation options 表格。

**Original:** If you answered `n` for "no" to the default (SQLite) database question, the CLI will ask for more questions about the database:

- Use arrow keys to select the database type you want, then press `Enter`.
- Give the database a name, define the database host address and port, define the database admin username and password, and define whether the database will use a SSL connection. For any of these questions, if you press `Enter` without typing anything, the default value (indicated in parentheses in the terminal output) will be used.

Once all questions have been answered, the script will start creating the Strapi project.

**中文译文:** 如果在默认 database（SQLite）问题中输入 `n` 表示 “no”，CLI 会继续询问 database 配置：

- 使用方向键选择 database 类型，然后按 `Enter`；
- 配置 database name、host address、port、administrator username、password，以及是否使用 SSL connection。对于这些问题，如果直接按 `Enter` 而不输入内容，将采用 terminal 中括号标示的默认值。

完成所有问题后，脚本会开始创建 Strapi 项目。

### CLI installation options

**Original:** The above installation guide only covers the basic installation option using the CLI. There are other options that can be used when creating a new Strapi project, for example:

**中文译文:** 上面的流程只覆盖最基本的 CLI 安装方式。创建 Strapi 项目时还可以使用以下 options：

| Option | Original description | 中文说明 |
|---|---|---|
| `--no-run` | Do not start the application after it is created | 创建完成后不启动 application。 |
| `--ts` / `--typescript` | Initialize the project with TypeScript (default) | 使用 TypeScript 初始化项目（默认）。 |
| `--js` / `--javascript` | Initialize the project with JavaScript | 使用 JavaScript 初始化项目。 |
| `--use-npm` | Force the usage of npm as the project package manager | 强制使用 npm 作为项目 package manager。 |
| `--use-pnpm` | Force the usage of pnpm as the project package manager | 强制使用 pnpm 作为项目 package manager。 |
| `--install` | Install all dependencies, skipping the related CLI prompt | 安装全部 dependencies，并跳过相关 CLI prompt。 |
| `--no-install` | Do not install all dependencies, skipping the related CLI prompt | 不安装 dependencies，并跳过相关 CLI prompt。 |
| `--git-init` | Initialize a git repository, skipping the related CLI prompt | 初始化 Git repository，并跳过相关 CLI prompt。 |
| `--no-git-init` | Do not initialize a git repository, skipping the related CLI prompt | 不初始化 Git repository，并跳过相关 CLI prompt。 |
| `--example` | Add example data, skipping the related CLI prompt | 添加 example data，并跳过相关 CLI prompt。 |
| `--no-example` | Do not add example data, skipping the related CLI prompt | 不添加 example data，并跳过相关 CLI prompt。 |
| `--skip-cloud` | Skip Strapi login and project creation steps | 跳过 Strapi login 与 Cloud project creation 步骤。 |
| `--non-interactive` | Skip all interactive prompts and use defaults (TypeScript, install dependencies, initialize git, SQLite database, no A/B tests). The `<directory>` argument is required when using this flag. | 跳过全部交互 prompt，并采用默认值：TypeScript、安装 dependencies、初始化 Git、SQLite database、不参与 A/B tests。使用该 flag 时必须提供 `<directory>`。 |
| `--enable-ab-tests` / `--no-enable-ab-tests` | Enable or disable anonymous A/B testing, skipping the related CLI prompt | 启用或禁用 anonymous A/B testing，并跳过相关 CLI prompt。 |
| `--skip-db` | Skip all database-related prompts and create a project with the default (SQLite) database | 跳过全部 database prompts，并使用默认 SQLite database 创建项目。 |
| `--template <template-name-or-url>` | Create the application based on a given template | 基于指定 template 创建 application。更多选项参见 templates 文档。 |
| `--dbclient <dbclient>` | Define the database client: `sqlite` (default), `postgres`, or `mysql` | 设置 database client：`sqlite`（默认）、`postgres` 或 `mysql`。 |
| `--dbhost <dbhost>` | Define the database host | 设置 database host。 |
| `--dbport <dbport>` | Define the database port | 设置 database port。 |
| `--dbname <dbname>` | Define the database name | 设置 database name。 |
| `--dbusername <dbusername>` | Define the database username | 设置 database username。 |
| `--dbpassword <dbpassword>` | Define the database password | 设置 database password。 |
| `--dbssl <dbssl>` | Define that SSL is used with the database, by passing `--dbssl=true` (No SSL by default) | 通过 `--dbssl=true` 指定 database 使用 SSL；默认不使用 SSL。 |
| `--dbfile <dbfile>` | For SQLite databases, define the database file path | 对 SQLite database，设置 database file path。 |
| `--quickstart` | Deprecated in Strapi 5. Directly create the project in quickstart mode. Use `--non-interactive` instead. | **Strapi 5 已弃用。** 过去用于直接以 quickstart mode 创建项目；现在使用 `--non-interactive`。 |

**Original:**
- If you do not pass a `--use-npm|pnpm` option, the installation script will use whatever package manager was used with the create command to install all dependencies (e.g., `npm create strapi` will install all the project's dependencies with npm).
- For additional information about database configuration, please refer to the database configuration documentation.
- Experimental Strapi versions are released every Tuesday through Saturday at midnight GMT. You can create a new Strapi application based on the latest experimental release using `npx create-strapi@experimental`. Please use these experimental builds at your own risk. It is not recommended to use them in production.

**中文译文:**
- 如果没有传入 `--use-npm|pnpm`，安装脚本会沿用执行 create command 时所使用的 package manager 来安装全部 dependencies。例如 `npm create strapi` 会使用 npm 安装项目 dependencies；
- Database 配置的更多信息参见 [database configuration](/cms/configurations/database)；
- Experimental Strapi versions 会在每周二至周六 GMT 午夜发布。可以使用 `npx create-strapi@experimental` 基于最新 experimental release 创建 application。Experimental builds 风险由使用者自行承担，不建议用于 production。

### Skipping the Strapi login step

**Original:** When the installation script runs, the terminal will first ask you if you want to login/signup. Choosing `Login/signup` will provide you with a 30-day trial of the Growth plan that will be automatically applied to your created project. This will give you access to advanced CMS features.

**中文译文:** 安装脚本启动后，terminal 首先询问是否 login/signup。选择 `Login/signup` 后，新项目会自动获得 30 天 Growth plan trial，从而可以使用更高级的 CMS features。

**Original:** If you prefer skipping this Strapi login part, use the arrow keys to select `Skip`. The script will resume and create a local project using the CMS Free plan.

**中文译文:** 如果希望跳过 Strapi login，使用方向键选择 `Skip`。脚本会继续执行，并使用 CMS Free plan 创建本地项目。

**Original:** You will be able to purchase a CMS license later by checking out our pricing page.

**中文译文:** 之后仍可通过 Strapi [pricing page](https://strapi.io/pricing-self-hosted) 购买 CMS license。

### Hosting your project

**Original:** You can deploy a project to Strapi Cloud. To host it online, you can choose to:

- host it yourself by pushing the project's code to a repository (e.g., on GitHub) before following the deployment guide,
- or use the Cloud CLI commands to log in to Strapi Cloud, link your local project to an existing Strapi Cloud project, and deploy it there.

**中文译文:** 可以将项目部署到 Strapi Cloud。若要让项目在线运行，可以选择：

- 自行托管：先将项目代码推送到 repository（例如 GitHub），再按照 [deployment guide](/cms/deployment) 部署；
- 使用 [Cloud CLI](/cloud/cli/cloud-cli)：登录 Strapi Cloud，将本地项目关联到已有 Strapi Cloud project，然后完成 deployment。

**Original:** If you want to host your project yourself and are not already familiar with GitHub, the documentation includes the steps required to push your Strapi project code to GitHub.

**中文译文:** 如果准备自行托管项目、但还不熟悉 GitHub，可以参见项目中的 [Push to GitHub 对照翻译](../../snippets/push-to-github.md)。

## Running Strapi

**Original:** To start the Strapi application, run the following command in the project folder:

```bash
npm run develop
```

**中文译文:** 在项目目录中运行以下命令启动 Strapi application：

```bash
npm run develop
```

**Original:** For self-hosted Strapi projects, all your content is saved in a database file (by default, SQLite) found in the `.tmp` subfolder in your project's folder. So anytime you start the Strapi application from the folder where you created your Strapi project, your content will be available.

**中文译文:** 对 self-hosted Strapi projects，全部内容都存储在 database 中；默认 SQLite database file 位于项目目录的 `.tmp` 子目录。因此，只要从创建 Strapi 项目的目录启动 application，就可以访问已有内容。

**Original:** If the content was added to a Strapi Cloud project, it is stored in the database managed with your Strapi Cloud project.

**中文译文:** 如果内容是在 Strapi Cloud project 中添加的，则会存储在该 Strapi Cloud project 管理的 database 中。更多信息参见 [Cloud database configuration](/cloud/advanced/database)。
