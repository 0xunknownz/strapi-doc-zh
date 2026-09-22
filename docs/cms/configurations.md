# 📖 对照翻译：Configuration

> Source: `docusaurus/docs/cms/configurations.md`  
> Upstream SHA: `d781b59c7943925b2f0679b4836bc307d662615a`

**Original:** Strapi applications are configured through files in the `/config` folder, including required base configurations for database, server, admin panel, middlewares, and API, plus optional configurations for plugins, TypeScript, API tokens, lifecycle functions, cron jobs, and environment variables.

**中文译文:** Strapi application 的主要配置集中在 `/config` folder。这里既包含 database、server、admin panel、middlewares 等基础配置，也可以定义 API、plugins、TypeScript、cron、environment、SSO 与 feature flags 等扩展配置。

## Base configurations

**Original:** The following base configurations are available from `/config`.

**中文译文:** `/config` 中常见基础配置如下：

| Configuration | Path | 中文说明 |
|---|---|---|
| Database | `config/database` | 必需；database client、connection、pool 等 |
| Server | `config/server` | 必需；host、port、proxy、cron 等 server settings |
| Admin panel | `config/admin` | 必需；admin auth、URL、SSO、API token 等 |
| Middlewares | `config/middlewares` | 必需；global middleware loading order 与配置 |
| API calls | `config/api` | 可选；REST / Document Service 的全局参数、分页与 strict validation |

## Additional configuration

**Original:** Some features require dedicated configuration.

**中文译文:** 某些功能需要额外配置文件或入口：

| Feature | Location | 中文说明 |
|---|---|---|
| Plugins | `config/plugins` | 启用、禁用或覆盖 plugin / provider config |
| TypeScript | `tsconfig.json`、`src/admin/tsconfig.json`、可选 `config/typescript` | TypeScript compilation 与 Strapi-specific type generation |
| API tokens | `config/admin` | 使用 API token authentication 时配置 |
| Lifecycle functions | `/src/index` | `register`、`bootstrap`、`destroy` |
| Cron jobs | `config/server` + 可选 `cron-tasks` | 启用并声明 cron tasks |
| Environment | `config/env/<environment>/...` | 为不同 environment 覆盖配置 |
| SSO | `config/admin` | Enterprise SSO provider configuration |
| Feature flags | `config/features` | Future / stable flags |

**Original:** Built-in Upload/Media Library and Users & Permissions settings are still configured through `config/plugins`, and GraphQL has its own plugin configuration.

**中文译文:** Strapi 5 中部分历史上由 core plugin 实现的能力仍沿用 `config/plugins`：
- Media Library / Upload；
- Users & Permissions；
- GraphQL plugin 的详细配置也从该入口加载。

## Guides

**Original:** Configuration guides cover custom RBAC conditions, environment-variable casting, and reading configuration values from code.

**中文译文:** 配置相关实战指南包括：
- [创建自定义 RBAC condition](/cms/configurations/guides/rbac)；
- [读取并转换 environment variables](/cms/configurations/guides/access-cast-environment-variables)；
- [在代码中访问 configuration values](/cms/configurations/guides/access-configuration-values)。
