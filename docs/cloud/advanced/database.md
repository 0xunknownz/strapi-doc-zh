# 📖 对照翻译：Cloud database configuration

> Source: `docusaurus/docs/cloud/advanced/database.md`  
> Upstream SHA: `60c2bbb69fae71c12a2161eb91cd0f70cc128c4c`

**Original:** Cloud database configuration

**中文译文:** Cloud 数据库配置

**Original:** Default PostgreSQL can be swapped for any supported SQL database by aligning configuration and environment variables.

**中文译文:** 通过正确配置项目与环境变量，可以把默认 PostgreSQL 替换为任意受支持的 SQL 数据库。

**Original:** Strapi Cloud provides a pre-configured PostgreSQL database by default. However, you can also configure it to utilize an external SQL database, if needed.

**中文译文:** Strapi Cloud 默认提供已经预配置好的 PostgreSQL 数据库。如有需要，也可以将项目配置为使用外部 SQL 数据库。

**Original:** Prerequisites:

- A local Strapi project running on `v4.8.2+`.
- Credentials for an external database.
- If using an existing database, the schema must match the Strapi project schema.

**中文译文:** 前置条件：

- 本地 Strapi 项目运行在 `v4.8.2+`；
- 拥有外部数据库的连接凭据；
- 如果使用已有数据库，其 schema 必须与 Strapi 项目 schema 匹配。

**Original:** While it's possible to use an external database with Strapi Cloud, you should do it while keeping in mind the following considerations:

- Strapi Cloud already provides a managed database that is optimized for Strapi.
- Using an external database may result in unexpected behavior and/or performance issues (e.g., network latency may impact performance). For performance reasons, it's recommended to host your external database close to the region where your Strapi Cloud project is hosted.
- Strapi can't provide security or support with external databases used with Strapi Cloud.

**中文译文:** 虽然 Strapi Cloud 可以使用外部数据库，但需要注意：

- Strapi Cloud 已经提供针对 Strapi 优化的托管数据库；
- 外部数据库可能带来不可预期的行为或性能问题，例如 network latency 会影响响应性能。为降低延迟，建议把外部数据库部署在尽可能接近 Strapi Cloud 项目 region 的位置；项目所在 region 可在 [Project Settings > General > Selected Region](/cloud/projects/settings#general) 中查看；
- Strapi 无法为在 Strapi Cloud 中使用的外部数据库提供安全保障或支持服务。

**Original:** Any environment variable added to your project that starts with `DATABASE_` will cause Strapi Cloud to assume that you will be using an external database and all Strapi Cloud specific database variables will not be injected!

**中文译文:** 只要项目中添加了任何以 `DATABASE_` 开头的 environment variable，Strapi Cloud 就会认为项目将使用外部数据库，并且**不会再注入 Strapi Cloud 自身的数据库变量**。

## Configuration

**Original:** The project `/config/database.js` or `/config/database.ts` file must match the configuration found in the environment variables in database configurations section.

**中文译文:** 项目的 `/config/database.js` 或 `/config/database.ts` 必须与 [environment variables in database configurations](https://docs.strapi.io/cms/configurations/database#environment-variables-in-database-configurations) 中描述的配置方式保持一致。

**Original:** Before pushing changes, add environment variables to the Strapi Cloud project:

1. Log into Strapi Cloud and click on the corresponding project on the Projects page.
2. Click on the **Settings** tab and choose **Variables** in the left menu.
3. Add the following environment variables:

| Variable | Value | Details |
| --- | --- | --- |
| `DATABASE_CLIENT` | your_db | Should be one of `mysql`, `postgres`, or `sqlite`. |
| `DATABASE_HOST` | your_db_host | The URL or IP address of your database host |
| `DATABASE_PORT` | your_db_port | The port to access your database |
| `DATABASE_NAME` | your_db_name | The name of your database |
| `DATABASE_USERNAME` | your_db_username | The username to access your database |
| `DATABASE_PASSWORD` | your_db_password | The password associated to this username |
| `DATABASE_SSL_REJECT_UNAUTHORIZED` | false | Whether unauthorized connections should be rejected |
| `DATABASE_SCHEMA` | public | - |

4. Click **Save**.

**中文译文:** 在 push 代码变更之前，先向 Strapi Cloud 项目添加 environment variables：

1. 登录 Strapi Cloud，在 *Projects* 页面进入目标项目；
2. 打开 **Settings**，在左侧菜单中选择 **Variables**；
3. 添加以下 environment variables：

| 变量 | 值 | 说明 |
| --- | --- | --- |
| `DATABASE_CLIENT` | your_db | 必须是 `mysql`、`postgres` 或 `sqlite` 之一。 |
| `DATABASE_HOST` | your_db_host | 数据库 host 的 URL 或 IP 地址。 |
| `DATABASE_PORT` | your_db_port | 数据库访问端口。 |
| `DATABASE_NAME` | your_db_name | 数据库名称。 |
| `DATABASE_USERNAME` | your_db_username | 数据库用户名。 |
| `DATABASE_PASSWORD` | your_db_password | 与用户名对应的密码。 |
| `DATABASE_SSL_REJECT_UNAUTHORIZED` | false | 是否拒绝未授权连接。 |
| `DATABASE_SCHEMA` | public | - |

4. 点击 **Save**。

**Original:** To ensure a smooth deployment, it is recommended to not change the names of the environment variables.

**中文译文:** 为确保 deployment 顺利进行，建议不要修改这些 environment variable 的名称。

## Deployment

**Original:** To deploy the project and utilize the external database, push the changes from earlier. This will trigger a rebuild and new deployment of the Strapi Cloud project.

**中文译文:** 要部署项目并启用外部数据库，请 push 前面完成的变更。这会触发 Strapi Cloud 项目的 rebuild 和新的 deployment。

**Original:** Once the application finishes building, the project will use the external database.

**中文译文:** 应用 build 完成后，项目就会开始使用外部数据库。

## Reverting to the default database

**Original:** To revert back to the default database, remove the previously added environment variables related to the external database from the Strapi Cloud project dashboard, and save. For the changes to take effect, you must redeploy the Strapi Cloud project.

**中文译文:** 若要恢复使用默认数据库，请在 Strapi Cloud 项目 dashboard 中删除之前添加的外部数据库相关 environment variables 并保存。要使变更生效，还必须重新部署 Strapi Cloud 项目。
