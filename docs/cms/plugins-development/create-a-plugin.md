# 📖 对照翻译：Plugin creation

> Source: `docusaurus/docs/cms/plugins-development/create-a-plugin.md`  
> Upstream SHA: `2d8f4649c8392dde3d63f91b720b8704aa1b1455`

**Original:** The recommended way to create a Strapi 5 plugin is the Plugin SDK, which can generate plugins independently of a Strapi project.

**中文译文:** Strapi 5 推荐使用 Plugin SDK 创建 plugin。Plugin 可以在 Strapi project 外独立开发，再通过 yalc / workspace link 到测试 application。

**Original:** `yalc` is required for the standard external-plugin linking workflow.

**中文译文:** 标准 `watch:link` workflow 需要全局安装 `yalc`：

```bash
npm install -g yalc
# or
yarn global add yalc
```

## Create a plugin

```bash
# Yarn
yarn dlx @strapi/sdk-plugin init my-strapi-plugin

# NPM
npx @strapi/sdk-plugin init my-strapi-plugin
```

**中文译文:** Path 可以是简单 folder name，也可以是完整相对路径。CLI 会通过 prompts 选择 TypeScript、admin/server parts 等，最终生成标准 plugin structure。

## Link to a Strapi project

**Original:** Use `watch:link`, then add the package with yalc from the target application.

**中文译文:** Plugin development 过程中推荐使用 `watch:link`；在另一个 terminal 中进入 Strapi project：

```bash
# Yarn
yarn dlx yalc add --link my-strapi-plugin && yarn install

# NPM
npx yalc add --link my-strapi-plugin && npm install
```

**中文译文:** 这里使用的是 plugin **package name**，不是 folder name。

**Original:** A plugin linked through `node_modules` is discovered automatically; it does not need an explicit local `resolve` entry.

**中文译文:** 通过 yalc 安装到 `node_modules` 后，Strapi 会自动发现 plugin，通常不需要在 `config/plugins` 额外写 local `resolve`。

## Build and verify

```bash
# Yarn
yarn build && yarn verify

# NPM
npm run build && npm run verify
```

**中文译文:** `build` 生成 publishable output，`verify` 检查结果是否符合 plugin package 要求。

## Upgrade SDK v5 → v6

**中文译文:**
- 删除旧 `packup.config.ts`；
- Build config 改由 `package.json#exports` 推导；
- 若需要 sourcemap，显式加 `--sourcemap`；
- 其他 plugin logic 通常无需改变。

## Monorepo

**Original:** Monorepos usually do not need `watch:link`; workspace linking handles symlinks, so use `watch`.

**中文译文:** Monorepo workspace 通常已经解决 package symlink，因此使用 `watch` 即可。若 admin code 需要直接指向 source，可在 bundler 中增加 alias。

**Original:** Server source still needs compilation, so `watch` is required for TypeScript plugin server code.

**中文译文:** 即使 monorepo 已 link package，plugin server TypeScript 仍需要编译；否则 Strapi server 无法读取未 transpile source。

## Local plugin configuration

```js title="/config/plugins.js|ts"
myplugin: {
  enabled: true,
  resolve: './src/plugins/local-plugin',
},
```

**Original:** If a local SDK plugin causes duplicated Strapi runtime errors, remove `@strapi/strapi` from the plugin's devDependencies.

**中文译文:** Local SDK plugin 如果出现 “X must be used within StrapiApp” 等 duplicated-runtime error，检查 plugin 是否自己安装了一份 `@strapi/strapi` dev dependency。移除它可确保 plugin 与 host application 使用同一 Strapi core instance。

## Local monorepo plugin without SDK

**Original:** Create root `strapi-server.js` and `strapi-admin.js` entry files.

**中文译文:** 不使用 Plugin SDK 时，可在 plugin root 手工创建：
- `strapi-server.js`
- `strapi-admin.js`

这两个 entry point 必须是 **JavaScript** 文件；server entry 不会自动 transpile `.ts`，admin detection 也只识别 `strapi-admin.js`。

```js
module.exports = () => ({
  register,
  config,
  controllers,
  contentTypes,
  routes,
});
```

```js
export default {
  register(app) {},
  bootstrap() {},
  registerTrads({ locales }) {},
};
```
