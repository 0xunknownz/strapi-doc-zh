# 📖 对照翻译：Docker environment variables

> Source: `docusaurus/docs/snippets/docker-env-table.md`  
> Upstream SHA: `eae23805e38ec315566fe7cbee570cbc0395dd71`

**Original:** The following environment variables are required in order to run Strapi in a Docker container:

**中文译文:** 要在 Docker container 中运行 Strapi，需要配置以下 environment variables：

**Original:**

| Variable name | Description |
|---|---|
| `NODE_ENV` | The environment in which the application is running. |
| `DATABASE_CLIENT` | The database client to use. |
| `DATABASE_HOST` | The database host. |
| `DATABASE_PORT` | The database port. |
| `DATABASE_NAME` | The database name. |
| `DATABASE_USERNAME` | The database username. |
| `DATABASE_PASSWORD` | The database password. |
| `JWT_SECRET` | The secret used to sign the JWT for the Users-Permissions plugin. |
| `ADMIN_JWT_SECRET` | The secret used to sign the JWT for the Admin panel. |
| `APP_KEYS` | The secret keys used to sign the session cookies. |
| `API_TOKEN_SALT` | The salt used to generate API tokens. |
| `TRANSFER_TOKEN_SALT` | The salt used to generate transfer tokens. |
| `ENCRYPTION_KEY` | The key used to encrypt secrets stored in the database (e.g., provider credentials configured through the admin panel). |

**中文译文:**

| Variable name | 说明 |
|---|---|
| `NODE_ENV` | 应用当前运行的 environment。 |
| `DATABASE_CLIENT` | 使用的 database client。 |
| `DATABASE_HOST` | Database host。 |
| `DATABASE_PORT` | Database port。 |
| `DATABASE_NAME` | Database name。 |
| `DATABASE_USERNAME` | Database username。 |
| `DATABASE_PASSWORD` | Database password。 |
| `JWT_SECRET` | 用于为 Users-Permissions plugin 的 JWT 签名的 secret。 |
| `ADMIN_JWT_SECRET` | 用于为 Admin panel 的 JWT 签名的 secret。 |
| `APP_KEYS` | 用于签署 session cookies 的 secret keys。 |
| `API_TOKEN_SALT` | 用于生成 API tokens 的 salt。 |
| `TRANSFER_TOKEN_SALT` | 用于生成 transfer tokens 的 salt。 |
| `ENCRYPTION_KEY` | 用于加密存储在 database 中的 secrets，例如通过 admin panel 配置的 provider credentials。 |

**Original:** You can also set some optional environment variables.

**中文译文:** 还可以配置一些 [可选 environment variables](/cms/configurations/environment#strapi)。
