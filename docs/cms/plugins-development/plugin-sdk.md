# 📖 对照翻译：Plugin SDK reference

> Source: `docusaurus/docs/cms/plugins-development/plugin-sdk.md`  
> Upstream SHA: `0846d43bf132737d39fd9bff04e0894e078fef26`

**Original:** The Plugin SDK provides commands for creating, building, watching, linking, verifying, and publishing Strapi plugins.

**中文译文:** `@strapi/sdk-plugin` 提供完整 plugin development CLI，用于初始化、build、watch、link、verify，最终发布 npm / Marketplace。

## `npx @strapi/sdk-plugin init`

```bash
npx @strapi/sdk-plugin init
```

**中文译文:** 在指定 path 初始化一个新 plugin。默认 path 为 `./src/plugins/my-plugin`，也支持 `--debug` / `--silent`。

## `strapi-plugin build`

```bash
strapi-plugin build
```

**中文译文:** 为发布构建 plugin。常用 options：
- `--force`
- `--debug`
- `--silent`
- `--minify`
- `--sourcemap`

**Original:** SDK v6 derives build configuration from `package.json#exports`; no Vite/Rollup config is required.

**中文译文:** SDK v6 会自动从 `package.json#exports` 推导 build configuration，不再需要 `vite.config.ts`、`rollup.config.ts` 或旧 `packup.config.ts`。

## `watch:link`

```bash
strapi-plugin watch:link
```

**中文译文:** Watch source、自动 rebuild，并执行 `yalc push --publish`，适合把外部 plugin 实时链接到测试用 Strapi project。

## `watch`

```bash
strapi-plugin watch
```

**中文译文:** 只 watch/rebuild，不做 yalc push，常用于 monorepo workspace 已自行处理 symlink 的场景。

## `verify`

```bash
strapi-plugin verify
```

**中文译文:** 在发布前检查 plugin build output 是否有效。

## SDK v5 compatibility

**Original:** SDK v5 can still be pinned for legacy `@strapi/pack-up` / `packup.config.ts` workflows, but v6 is recommended.

**中文译文:** 如必须保留旧 `@strapi/pack-up` / `packup.config.ts` build system，可安装：

```bash
yarn add @strapi/sdk-plugin@5
# or
npm install @strapi/sdk-plugin@5
```

但官方推荐 v6，以获得安全更新和简化配置。
