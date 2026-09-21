# 📖 对照翻译：Installation prerequisites

> Source: `docusaurus/docs/snippets/installation-prerequisites.md`  
> Upstream SHA: `13f6f7986d64db27d380b55f6fab2d8bedbd281c`

**Original:** Before installing Strapi, the following requirements must be installed on your computer:

**中文译文:** 安装 Strapi 之前，请确保你的计算机已经安装以下依赖：

**Original:**
- Node.js: Only Active LTS or Maintenance LTS versions are supported (currently `v22`, `v24`, and `v26`). Odd-number releases of Node, known as "current" versions of Node.js, are not supported (e.g. v23, v25).
- Your preferred Node.js package manager:
  - npm (`v6` and above)
  - pnpm (on Strapi Cloud, Corepack matches the pnpm version pinned in your project's `package.json` `packageManager` field, or uses Corepack's bundled default if none is pinned)
- Python (if using a SQLite database)
- A supported web browser: The Admin panel targets browsers matching the default Browserslist query: `last 3 major versions`, `Firefox ESR`, `last 2 Opera versions`, and `not dead`. See browsersl.ist for the current coverage matrix. Projects can override these defaults with a Browserslist configuration at the project root.

**中文译文:**
- Node.js：仅支持 Active LTS 或 Maintenance LTS 版本（当前为 `v22`、`v24` 和 `v26`）。不支持 Node.js 的奇数版本，也就是所谓的 “current” 版本，例如 `v23`、`v25`。
- 你偏好的 Node.js 包管理器：
  - npm（`v6` 及以上）
  - pnpm（在 Strapi Cloud 中，Corepack 会使用项目 `package.json` 的 `packageManager` 字段所锁定的 pnpm 版本；如果没有锁定版本，则使用 Corepack 自带的默认版本）
- Python（使用 SQLite 数据库时需要）
- 受支持的 Web 浏览器：管理面板以默认 Browserslist 查询所匹配的浏览器为目标，即 `last 3 major versions`、`Firefox ESR`、`last 2 Opera versions` 和 `not dead`。可通过 browsersl.ist 查看当前覆盖矩阵。项目也可以在项目根目录中使用 Browserslist 配置覆盖这些默认规则。
