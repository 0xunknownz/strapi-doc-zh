# 📖 对照翻译：Deployment

> Source: `docusaurus/docs/cms/deployment.md`  
> Upstream SHA: `0d0296c22335fab1dfc26ffd4e0481c086dbaa41`

**Original:** Deployment options cover hardware/software prerequisites, environment variable setup, and building the admin panel before launch, plus the principles a continuous deployment pipeline should respect.

**中文译文:** Deployment 文档涵盖 hardware / software 前置条件、environment variables 配置、上线前 build admin panel，以及 continuous deployment pipeline 应遵循的基本原则。

**Original:** Strapi provides many deployment options. Applications can be deployed on traditional hosting servers or a preferred hosting provider.

**中文译文:** Strapi 提供多种 deployment 方式。Strapi application 可以部署到传统 hosting server，也可以使用你选择的 hosting provider。

**Original:** You can use Strapi Cloud to quickly deploy and host your project.

**中文译文:** 如果希望快速部署与托管项目，可以直接使用 [Strapi Cloud](/cloud/intro)。

**Original:** If you created content structure/data locally, Data Management can transfer data between instances. Another workflow is to create schema locally, push code to Git, deploy to production, then add production content.

**中文译文:** 如果已经在本地使用 Content-Type Builder 创建 content structure，并通过 Content Manager 添加数据，可以使用 [Data Management](/cms/features/data-management) 在 Strapi instances 之间传输数据。另一种常见流程是先在本地定义 content structure，将代码 push 到 Git repository 并部署到 production，然后直接在 production instance 中录入正式内容。

**Original:** For self-hosted Kubernetes deployments, Strapi recommends npm rather than pnpm because aggressive dependency hoisting can break native modules.

**中文译文:** 对 self-hosted Kubernetes deployment，Strapi 建议使用 **npm** 而不是 **pnpm**。pnpm 激进的 dependency hoisting 可能导致 `mysql2` 等 native modules 无法正确加载；npm 更平坦、可预测的 `node_modules` 结构更适合这类部署。

## General guidelines

### Hardware and software requirements

**Original:** Requirements include installation prerequisites, standard OS build tools, server hardware, a supported database, and a supported operating system.

**中文译文:** Deployment 前需要满足：
- [Installation prerequisites](../snippets/installation-prerequisites.md)；
- 操作系统的标准 build tools（大多数 Debian-based 系统为 `build-essentials`）；
- [Hardware requirements](../snippets/hardware-require.md)；
- [Supported database versions](../snippets/supported-databases.md)；
- [Supported operating systems](../snippets/operating-system-require.md)。

**Original:** Database deployment is covered in the databases guide.

**中文译文:** Database 与 Strapi 一起部署的说明请参阅 [databases guide](/cms/configurations/database#databases-installation)。

### Application Configuration

**Original:** Production configuration has 2 steps: configure through environment variables, then build the admin panel and launch the server.

**中文译文:** 将 Strapi application 配置为 production 运行主要有 2 步：先通过 environment variables 设置配置，然后 build admin panel 并启动 server。

#### 1. Configure

**Original:** Use environment variables to configure based on environment, for example:

```js title="/config/server.js"
module.exports = ({ env }) => ({
  host: env('HOST', '0.0.0.0'),
  port: env.int('PORT', 1337),
});
```

**中文译文:** 建议使用 environment variables 根据 environment 配置 application。上面的 `/config/server.js` 示例保持原样。

**Original:** Strapi generates a `.env` with defaults. Edit it or define variables in your deployment platform:

```
HOST=10.0.0.1
PORT=1338
```

**中文译文:** Strapi 创建新项目时会生成包含默认值的 `.env`。可以编辑该文件，也可以在 deployment platform 中设置对应 variables。更多信息参阅 [environment configuration](/cms/configurations/environment)。

#### 2. Launch the server

**Original:** Before running in production, build the admin panel with `NODE_ENV=production`.

**中文译文:** 在 production 中启动 server 前，需要先以 `NODE_ENV=production` build admin panel：

```bash
# yarn
NODE_ENV=production yarn build

# npm
NODE_ENV=production npm run build
```

**Original:** On Windows, install `cross-env`, add a build script, and run it.

**中文译文:** Windows 中可以安装 `cross-env`：

```bash
npm install --save-dev cross-env
```

并在 `package.json` scripts 中加入：

```json
"build:win": "cross-env NODE_ENV=production npm run build"
```

然后运行：

```bash
npm run build:win
```

**Original:** Start the server with production settings.

**中文译文:** 使用 production settings 启动 server：

```bash
# yarn
NODE_ENV=production yarn start

# npm
NODE_ENV=production npm run start
```

Windows 可类似配置：

```json
"start:win": "cross-env NODE_ENV=production npm run start"
```

并运行 `npm run start:win`。

**Original:** A process manager such as PM2 is strongly recommended.

**中文译文:** Production 中强烈建议使用 [PM2](/cms/deployment/guides/pm2) 等 process manager 管理 Strapi process。

**Original:** If you need `node server.js` instead of npm start, create:

```js title="./server.js"
const strapi = require('@strapi/strapi');
strapi.createStrapi(/* {...} */).start();
```

**中文译文:** 如果需要通过 `node server.js` 启动，而不是 `npm run start`，可以创建上面的 `./server.js`。TypeScript project 使用 `createStrapi` 时还必须提供 `distDir` option。

**Original:** Strapi exposes `/_health`. When ready it returns HTTP 204 No Content and a `strapi: You are so French!` header.

**中文译文:** Strapi 内置轻量 health check endpoint：`/_health`。Server ready 后会返回 HTTP `204 No Content`，并包含 `strapi: You are so French!` header，可用于 uptime monitor 与 load balancer 健康检查。

### Advanced configurations

**Original:** Admin and API can be hosted on different servers; see the dedicated configuration.

**中文译文:** 如果希望把 administration panel 与 API 部署在不同 server，请参阅 [对应配置](/cms/configurations/admin-panel#deploy-on-different-servers)。

## Continuous deployment

**Original:** Build/start steps are what deployment pipelines automate. Strapi does not require a specific CI tool; GitHub Actions, GitLab CI, Jenkins, or provider build systems can all work.

**中文译文:** 上述 build / start steps 正是 deployment pipeline 需要自动化的内容。Strapi 不要求使用特定 CI tool；GitHub Actions、GitLab CI、Jenkins 或 hosting provider 自带 build system 都可以，只要能够安装 dependencies、build admin panel 并运行 server。

**Original:** Example GitHub Actions workflow:

```yaml title=".github/workflows/deploy.yml"
name: Deploy

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: yarn

      - run: yarn install --frozen-lockfile

      - run: yarn build
        env:
          NODE_ENV: production
          APP_KEYS: ${{ secrets.APP_KEYS }}
          API_TOKEN_SALT: ${{ secrets.API_TOKEN_SALT }}
          ADMIN_JWT_SECRET: ${{ secrets.ADMIN_JWT_SECRET }}
          JWT_SECRET: ${{ secrets.JWT_SECRET }}
          TRANSFER_TOKEN_SALT: ${{ secrets.TRANSFER_TOKEN_SALT }}
          ENCRYPTION_KEY: ${{ secrets.ENCRYPTION_KEY }}

      # Add your provider's deployment step here
```

**中文译文:** 上面的 GitHub Actions 示例会在每次 push 到 `main` 时执行 build，并在 build step 中设置 production 环境与 secrets。真正 deployment step 取决于 hosting provider，因此示例停在 build 阶段。YAML 保持原样。

**Original:** Pipeline principles:
- Build admin panel with `NODE_ENV=production`; rebuild when code/admin configuration changes.
- Inject secrets from CI, never committed `.env`.
- Keep the same secrets across deployments for an environment; regenerating key JWT secrets invalidates sessions/tokens.
- Isolate environments; staging must not use production DB.
- Account for schema sync and review schema changes before production.

**中文译文:** 任意 Strapi pipeline 都应遵循：
- 在 pipeline 中以 `NODE_ENV=production` build admin panel；代码或 admin configuration 变化后需要重新 build；
- Secrets 应通过 CI tool 注入，**不要**提交包含真实 secret 的 `.env`。至少 `APP_KEYS`、`API_TOKEN_SALT`、`ADMIN_JWT_SECRET`、`JWT_SECRET`、`TRANSFER_TOKEN_SALT`、`ENCRYPTION_KEY` 和 database credentials 需要在 build 与运行 server 时可用；
- 同一个 environment 的多次 deployment 应保持相同 secrets。重新生成 `APP_KEYS`、`ADMIN_JWT_SECRET` 或 `JWT_SECRET` 可能使现有 sessions / API tokens 失效；
- Environments 必须隔离，staging pipeline 不应连接 production database；
- 要考虑 schema sync：修改 content-types schema 后启动 Strapi 会修改 database；删除 content-type 会 drop 对应 table。上线前应审查 schema changes，详见 [Database migrations](/cms/database-migrations)。

**Original:** Content types travel with code, not data. They cannot be created/updated in production; schema changes must be deployed with code. Data should be moved with Data Management.

**中文译文:** Content-types 随**代码**而不是随 data 迁移。在 production 中不能创建或更新 content-types，因此 schema changes 必须通过 deployment code 带入。不同 environments 之间的数据应通过 [Data Management](/cms/features/data-management/transfer) 迁移。

**Original:** Strapi Cloud handles this pipeline automatically on every push to the tracked branch.

**中文译文:** [Strapi Cloud](/cloud/intro) 可以代管整套 pipeline：它会在 tracked branch 每次 push 后自动 [build 和 deploy](/cloud/getting-started/deployment)，无需自行维护 workflow file。

## Deployment guides

**Original:** Before following deployment guides, your project should be created and you should read the general guidelines.

**中文译文:** 使用下面的 deployment guides 前，请先创建 Strapi 项目，并阅读本页 general deployment guidelines。

**Original:** Guides cover Caddy, HAProxy, Nginx, Traefik, and PM2.

**中文译文:** 官方指南包括：
- [Caddy reverse proxy](/cms/deployment/guides/caddy)；
- [HAProxy](/cms/deployment/guides/haproxy)；
- [Nginx reverse proxy](/cms/deployment/guides/nginx)；
- [Traefik](/cms/deployment/guides/traefik)；
- [PM2 process manager](/cms/deployment/guides/pm2)。

**Original:** Strapi's integrations page also covers AWS, Azure, DigitalOcean App Platform, Heroku, plus external community deployment guides.

**中文译文:** Strapi integrations 页面还提供 AWS、Azure、DigitalOcean App Platform、Heroku 等第三方 deployment 信息；此外也可参考社区维护的其他 hosting guide。

**Original:** For multi-tenancy options, see the Strapi Blog guide.

**中文译文:** 如果需要 multi-tenancy 方案，可以参考 Strapi Blog 的相关 comprehensive guide。
