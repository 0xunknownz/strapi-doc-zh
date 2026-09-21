# 📖 对照翻译：Environment configuration and variables

> Source: `docusaurus/docs/cms/configurations/environment.md`  
> Upstream SHA: `e0efe10b1502ca74e824eac0a25730cfbc877d93`

**Original:** Strapi-specific environment variables and `.env` usage enable per-environment configs, with `env()` helpers for casting values.

**中文译文:** Strapi 提供专用 environment variables，并支持通过 `.env` 实现不同 environment 的配置；`env()` helper 还可以读取变量并将值转换为不同类型。

**Original:** Strapi provides specific environment variable names. Defining them in an environment file (e.g., `.env`) will make these variables and their values available in your code.

**中文译文:** Strapi 定义了一组专用 environment variable names。将这些变量写入 environment file（例如 `.env`）后，就可以在项目代码中访问对应变量和值。

**Original:** An `env()` utility can be used to retrieve environment variables and cast them to different types. You can also create configurations specific to different environments.

**中文译文:** 可以使用 `env()` utility [读取 environment variables](/cms/configurations/guides/access-cast-environment-variables#accessing-environment-variables)，并将它们 [cast 为不同类型](/cms/configurations/guides/access-cast-environment-variables)。除此之外，还可以创建针对不同 environment 的独立配置。

## Strapi's environment variables

**Original:**

| Setting | Description | Type | Default value |
|---|---|---|---|
| `STRAPI_TELEMETRY_DISABLED` | Don't send telemetry usage data to Strapi | Boolean | `false` |
| `ADMIN_PATH` | Path the admin panel is served under. Defaults to the pathname of `admin.url` and is injected into the admin JS bundle at build time. | String | `'/admin'` |
| `STRAPI_ADMIN_BACKEND_URL` | URL the admin panel uses to reach the back-end server. It is injected into the admin JS bundle at build time. | String | auto-derived |
| `STRAPI_LICENSE` | License key to activate Enterprise Edition | String | `undefined` |
| `NODE_ENV` | Type of environment where the application is running | String | `'development'` |
| `BROWSER` | Open the admin panel in the browser after startup | Boolean | `true` |
| `ENV_PATH` | Path to the file containing environment variables | String | `'./.env'` |
| `STRAPI_PLUGIN_I18N_INIT_LOCALE_CODE` | Initialization locale when i18n is enabled | String | `'en'` |
| `STRAPI_ENFORCE_SOURCEMAPS` | Force bundler to emit source maps | boolean | `false` |
| `FAST_REFRESH` | Webpack-only Fast Refresh switch | boolean | `true` |
| `HOST` | Address the Strapi server listens on | String | `0.0.0.0` |
| `PORT` | Port used by Strapi server | Number | `1337` |
| `APP_KEYS` | Comma-separated keys used to sign cookies and other secrets | String | auto-generated |
| `API_TOKEN_SALT` | Salt used for API tokens | String | auto-generated |
| `ADMIN_JWT_SECRET` | Secret for admin-panel JWT tokens | String | auto-generated |
| `JWT_SECRET` | Secret for Users & Permissions JWT tokens | String | auto-generated |
| `TRANSFER_TOKEN_SALT` | Salt for Data Management transfer tokens | String | auto-generated |
| `DATABASE_CLIENT` | Database client, e.g. `sqlite` | String | `sqlite` |
| `DATABASE_FILENAME` | SQLite database file location | String | `.tmp/data.db` |

**中文译文:**

| 设置项 | 说明 | 类型 | 默认值 |
|---|---|---|---|
| `STRAPI_TELEMETRY_DISABLED` | 禁止向 Strapi 发送 telemetry usage data。 | Boolean | `false` |
| `ADMIN_PATH` | Admin panel 的挂载 path；默认取 `admin.url` 的 pathname，并在 build 时注入 admin JS bundle。 | String | `'/admin'` |
| `STRAPI_ADMIN_BACKEND_URL` | Admin panel 访问 back-end server 使用的 URL；在 build 时注入 admin JS bundle。 | String | 自动推导 |
| `STRAPI_LICENSE` | 激活 Enterprise Edition 的 license key。 | String | `undefined` |
| `NODE_ENV` | Application 当前运行的 environment 类型；`production` 会启用生产环境行为。 | String | `'development'` |
| `BROWSER` | 启动后是否自动在 browser 中打开 admin panel。 | Boolean | `true` |
| `ENV_PATH` | Environment variables 文件路径。 | String | `'./.env'` |
| `STRAPI_PLUGIN_I18N_INIT_LOCALE_CODE` | i18n 启用时 application 的初始化 locale。 | String | `'en'` |
| `STRAPI_ENFORCE_SOURCEMAPS` | 强制 bundler 输出 source maps。 | boolean | `false` |
| `FAST_REFRESH` | 仅 webpack：启用 Fast Refresh。 | boolean | `true` |
| `HOST` | Strapi server 监听地址。 | String | `0.0.0.0` |
| `PORT` | Strapi server 使用的 port。 | Number | `1337` |
| `APP_KEYS` | 用于签署 cookies 与其他 secrets 的逗号分隔 keys。 | String | 自动生成 |
| `API_TOKEN_SALT` | 创建 API tokens 使用的 salt。 | String | 自动生成 |
| `ADMIN_JWT_SECRET` | Admin panel JWT token secret；默认启用 admin panel 时需要。 | String | 自动生成 |
| `JWT_SECRET` | Users & Permissions 生成 JWT 使用的 secret。 | String | 自动生成 |
| `TRANSFER_TOKEN_SALT` | Data Management transfer token 使用的 salt。 | String | 自动生成 |
| `DATABASE_CLIENT` | Database client，例如 `sqlite`。 | String | `sqlite` |
| `DATABASE_FILENAME` | SQLite database file 的位置。 | String | `.tmp/data.db` |

**Original:** Prefixing an environment variable with `STRAPI_ADMIN_` exposes it to the admin front end when the admin panel is built from your project. Strapi Cloud does not expose `STRAPI_ADMIN_*` variables to the admin front end.

**中文译文:** 在 self-hosted 等由项目自身 build admin panel 的场景中，environment variable 名称添加 `STRAPI_ADMIN_` 前缀，可以把变量暴露给 admin front end，例如 `STRAPI_ADMIN_MY_PLUGIN_VARIABLE` 可通过 `process.env.STRAPI_ADMIN_MY_PLUGIN_VARIABLE` 访问。**Strapi Cloud 不会把 `STRAPI_ADMIN_*` variables 暴露给 admin front end。**

### Example `.env` file

**Original:** The Strapi CLI generates `.env` and `.env.example` files containing security keys and database settings.

**中文译文:** Strapi CLI 会生成包含 security keys 和 database settings 的 `.env` 与 `.env.example`。完整示例参见 [sample-env](../../snippets/sample-env.md)。

**Original:** Set these environment variables for secure authentication with sessions management:

```bash title=".env"
# Admin authentication
ADMIN_JWT_SECRET=your-admin-secret-key

# Cookie domain (optional)
ADMIN_COOKIE_DOMAIN=yourdomain.com

# Users & Permissions JWT secret
JWT_SECRET=your-content-api-secret-key

# Users & Permissions session management
UP_JWT_MANAGEMENT=refresh  # or 'legacy-support'
UP_SESSIONS_ACCESS_TTL=604800  # 1 week in seconds
UP_SESSIONS_MAX_REFRESH_TTL=2592000  # 30 days in seconds
UP_SESSIONS_IDLE_REFRESH_TTL=604800  # 7 days in seconds
UP_SESSIONS_HTTPONLY=false  # true for HTTP-only cookies
UP_SESSIONS_COOKIE_NAME=strapi_up_refresh
UP_SESSIONS_COOKIE_SAMESITE=lax
UP_SESSIONS_COOKIE_PATH=/
UP_SESSIONS_COOKIE_SECURE=false  # true in production
```

**中文译文:** 若使用 [sessions management](/cms/features/users-permissions#jwt-management-modes)，可通过上面的 environment variables 配置安全 authentication。变量名和值示例保持原样。

## Environment configurations

**Original:** Environment-specific configurations follow `./config/env/{environment}/{filename}`. They are useful for static configuration differences where environment variables are not ideal.

**中文译文:** Environment-specific configuration 使用 `./config/env/{environment}/{filename}` 命名与目录结构。当不同 environments 之间存在静态配置差异、但不适合通过 environment variables 处理时，这种方式很有用。

**Original:** Environment-specific configuration is merged into base configuration in `./config`. The environment is selected by `NODE_ENV`, which defaults to `development`.

**中文译文:** Environment-specific configuration 会合并到 `./config` 中的 base configuration。具体加载哪个 environment 由 `NODE_ENV` 决定，默认值为 `development`。

**Original:** With `NODE_ENV=production`, Strapi loads both `./config/*` and `./config/env/production/*`. Production-specific values override defaults.

**中文译文:** 当 `NODE_ENV=production` 时，Strapi 会同时加载 `./config/*` 与 `./config/env/production/*`；production-specific configuration 会覆盖 base configuration 中的同名设置。结合 environment variables 后，可以实现灵活的多环境配置。

**Original code (kept unchanged):**

```js title="./config/server.js"
module.exports = {
  host: '127.0.0.1',
};
```

```js title="./config/env/production/server.js"
module.exports = ({ env }) => ({
  host: env('HOST', '0.0.0.0'),
});
```

```ts title="./config/server.ts"
export default ({ env }) => ({
  host: '127.0.0.1',
});
```

```ts title="./config/env/production/server.ts"
export default ({ env }) => ({
  host: env('HOST', '0.0.0.0'),
});
```

**中文译文:** 上面的 JavaScript / TypeScript 示例保持原样：默认 host 为 `127.0.0.1`，production 中通过 `HOST` environment variable 覆盖，未设置时回退到 `0.0.0.0`。

**Original code (kept unchanged):**

```bash
yarn start
NODE_ENV=production yarn start
HOST=10.0.0.1 NODE_ENV=production yarn start
```

**中文译文:** 第一条使用默认 `127.0.0.1`；第二条使用 `.env` 中的 production `HOST`，未定义则为 `0.0.0.0`；第三条显式使用 `10.0.0.1`。

**Original:** For more details, see the Access and cast variables guide.

**中文译文:** 更深入的 environment variable 读取与类型转换方式，请参阅 [Access and cast variables](/cms/configurations/guides/access-cast-environment-variables)。
