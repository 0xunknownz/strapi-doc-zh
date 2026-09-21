# 📖 对照翻译：OpenAPI specification generation

> Source: `docusaurus/docs/cms/api/openapi.md`  
> Upstream SHA: `72c3aff82626d78fab17309a59c23e548dee15fc`

**Original:** Strapi provides a CLI tool to automatically generate OpenAPI 3.1.0 specifications documenting all API endpoints, parameters, and responses. The generated specification can be integrated with Swagger UI for interactive API documentation.

**中文译文:** Strapi 提供 CLI 工具，可自动生成 OpenAPI 3.1.0 specification，记录 Content API 的 endpoints、parameters 与 response schema。生成的 specification 还可以接入 Swagger UI，构建交互式 API documentation。

**Original:** The CLI creates comprehensive documentation for the Content API and can be integrated with tools such as Swagger UI.

**中文译文:** OpenAPI generator 会根据 Strapi application 当前 Content API 自动构建完整 specification，可用于 client generation、API schema review，以及 Swagger UI 等 documentation tooling。

**Original:** OpenAPI generation is experimental. Behavior and output may change without semantic-versioning guarantees.

**中文译文:** OpenAPI generation 当前属于 **Experimental feature**。其行为与输出格式仍可能变化，不保证所有变化都遵循 semantic versioning。

## Generating an OpenAPI specification

**Original:** The generator is included in Strapi core and requires no additional installation.

**中文译文:** OpenAPI generator 已包含在 Strapi core 中，无需安装额外 package。

### CLI usage

**Original:** Run without arguments to create `specification.json` in the project root.

```bash
# Yarn
yarn strapi openapi generate

# NPM
npm run strapi openapi generate
```

**中文译文:** 不传额外参数时，会在 Strapi project root 生成 `specification.json`。命令保持原样。

**Original:** Use `--output` to choose the path and filename.

```bash
# Yarn
yarn strapi openapi generate --output ./docs/api-spec.json

# NPM
npm run strapi openapi generate -- --output ./docs/api-spec.json
```

**中文译文:** 使用 `--output` 可以自定义生成文件的位置与名称。

**Original:** Known limitation: nested component fields marked required in the Admin panel might not have matching `required` metadata in the generated OpenAPI schema.

**中文译文:** 已知限制：Admin panel 中标记为 required 的 nested component inner field，在生成的 OpenAPI schema 中可能缺少对应 `required` metadata。因此依赖 raw OpenAPI schema 的 client generator 可能生成比 Strapi 实际 validation 更宽松的类型。当前应继续在 application code 中验证 nested payload，或使用 controller sanitization / validation helpers。

### Specification structure and content

**Original:** Generated files follow OpenAPI 3.1.0.

**中文译文:** 生成的 specification 遵循 [OpenAPI 3.1.0](https://spec.openapis.org/oas/v3.1.0.html)。

**Original example (kept unchanged):**

```json
{
  "openapi": "3.1.0",
  "x-powered-by": "strapi",
  "x-strapi-version": "5.21.0",
  "info": {
    "title": "My Strapi API",
    "description": "API documentation for My Strapi API",
    "version": "1.0.0"
  },
  "paths": {
    "/api/articles": {
      "get": {
        "operationId": "article/get/articles",
        "parameters": [
          {
            "name": "fields",
            "in": "query",
            "schema": {
              "type": "array",
              "items": { "type": "string" }
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Successful response",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": { "$ref": "#/components/schemas/Article" }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

**中文译文:** Specification 会包含 API metadata、`paths`、operation parameters、responses 与 reusable `components.schemas`。JSON 示例保持原样。

**Original:** Generated specs include CRUD routes for content types, custom API routes, authentication endpoints, upload endpoints, and plugin endpoints.

**中文译文:** 生成结果会涵盖：
- 所有 content types 的 CRUD routes；
- application 中定义的 custom API routes；
- user management / authentication endpoints；
- media upload endpoints；
- installed plugins 提供的 endpoints。

## Configuring HTTP endpoint access

**Original:** By default Strapi does not expose HTTP endpoints for the generated specification. Add an `openapi` key to `/config/server` to opt in.

**中文译文:** 默认情况下，Strapi **不会**通过 HTTP 暴露生成的 OpenAPI specification。若希望提供 live endpoint，需要在 `/config/server.js|ts` 中添加 `openapi` configuration。

| Sub-key | Endpoint | access | 默认 | 中文说明 |
|---|---|---|---|---|
| `content-api` | `GET /api/openapi.json` | `disabled` | 是 | 不注册 endpoint |
| `content-api` | `GET /api/openapi.json` | `public` | 否 | 无 authentication 公开访问 |
| `admin` | `GET /admin/openapi.json` | `disabled` | 是 | 不注册 endpoint |
| `admin` | `GET /admin/openapi.json` | `authenticated` | 否 | 仅 authenticated admin 可访问 |

**Original code (kept unchanged):**

```js title="/config/server.js"
module.exports = {
  openapi: {
    'content-api': {
      access: 'public',
    },
    admin: {
      access: 'authenticated',
    },
  },
};
```

```ts title="/config/server.ts"
export default {
  openapi: {
    'content-api': {
      access: 'public',
    },
    admin: {
      access: 'authenticated',
    },
  },
};
```

**中文译文:** 上例同时公开 Content API specification，并让 Admin specification 仅对 authenticated admin 开放。代码保持原样。

**Original:** `content-api.access='authenticated'` and `admin.access='public'` are invalid and cause startup errors.

**中文译文:** `content-api.access='authenticated'` 与 `admin.access='public'` 都不是支持的组合，配置后 Strapi 会在 startup 报错。

**Original:** Role-based access control for OpenAPI endpoints is not supported. Any authenticated admin can read the admin specification.

**中文译文:** OpenAPI endpoint 当前不支持细粒度 RBAC。Admin endpoint 使用 `admin::isAuthenticatedAdmin` policy，因此任何 authenticated admin user 都能读取完整 specification。

**Original:** A public Content API specification exposes the shape of the whole API, including content types that are not publicly readable.

**中文译文:** 如果将 Content API specification 设置为 public，它会向任何可访问 endpoint 的用户暴露**完整 Content API surface**，包括本身并未开放 public read permission 的 content types。如果不希望暴露 schema，应保持 `disabled` 并通过 CLI 生成静态文件。

### Endpoint options

| Option | Type | Default | 中文说明 |
|---|---|---|---|
| `route.path` | String | `'/openapi.json'` | specification 子路径；分别解析到 `/api` 或 `/admin` 下 |
| `cache.enabled` | Boolean | `true` | 是否启用 file-based cache |
| `cache.maxAgeMs` | Number | `60000` | cache 最大有效时间，毫秒 |
| `cache.filePath` | String | `.strapi/openapi/<type>.json` | cache file path，相对路径以 application root 为基准 |

**Original:** Content API and Admin OpenAPI endpoints must resolve to different full paths.

**中文译文:** `content-api` 与 `admin` endpoint 最终解析出的完整 URL 必须不同，否则 startup 会报错。

## Integrating with Swagger UI

**Original:** If an HTTP endpoint is exposed, Swagger UI can point directly to the live OpenAPI URL. Otherwise generate a static file.

**中文译文:** 如果已经开启 HTTP OpenAPI endpoint，可以让 Swagger UI 直接读取 live URL（例如 `/api/openapi.json`）；否则可先生成静态 specification file。

### 1. Generate specification

```bash
# Yarn
yarn strapi openapi generate --output ./public/swagger-spec.json

# NPM
npm run strapi openapi generate -- --output ./public/swagger-spec.json
```

### 2. Allow Swagger UI assets in CSP

**Original:** Update security middleware to allow scripts/styles from `https://unpkg.com`.

**中文译文:** Swagger UI 示例从 `unpkg.com` 加载 scripts / styles，因此需要修改 Strapi security middleware 的 Content Security Policy。核心 directives 如下，代码保持原样：

```js
{
  name: 'strapi::security',
  config: {
    contentSecurityPolicy: {
      useDefaults: true,
      directives: {
        'script-src': ["'self'", "'unsafe-inline'", 'https://unpkg.com'],
        'style-src': ["'self'", "'unsafe-inline'", 'https://unpkg.com'],
        'connect-src': ["'self'", 'https:'],
        'img-src': ["'self'", 'data:', 'blob:', 'https:'],
        'media-src': ["'self'", 'data:', 'blob:'],
        upgradeInsecureRequests: null,
      },
    },
  },
}
```

### 3. Create `public/openapi.html`

**Original code (kept unchanged):**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>API Documentation</title>
    <link
      rel="stylesheet"
      type="text/css"
      href="https://unpkg.com/swagger-ui-dist@5.0.0/swagger-ui.css"
    />
  </head>
  <body>
    <div id="swagger-ui"></div>
    <script src="https://unpkg.com/swagger-ui-dist@5.0.0/swagger-ui-bundle.js"></script>
    <script src="https://unpkg.com/swagger-ui-dist@5.0.0/swagger-ui-standalone-preset.js"></script>
    <script>
      window.onload = function () {
        SwaggerUIBundle({
          url: './swagger-spec.json',
          dom_id: '#swagger-ui',
          presets: [
            SwaggerUIBundle.presets.apis,
            SwaggerUIStandalonePreset
          ],
          layout: 'StandaloneLayout',
        });
      };
    </script>
  </body>
</html>
```

**中文译文:** 该页面加载 Swagger UI，并把 `./swagger-spec.json` 作为 specification source。若使用 live OpenAPI endpoint，可将 `url` 替换为对应 endpoint URL。

### 4. Restart Strapi

**Original:** Restart with `yarn develop` or `npm run develop`, then visit `/openapi.html`.

**中文译文:** 重启 Strapi（`yarn develop` 或 `npm run develop`），然后访问 `/openapi.html` 即可查看 Swagger UI。
