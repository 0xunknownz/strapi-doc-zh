# 📖 对照翻译：Admin panel bundlers

> Source: `docusaurus/docs/cms/admin-panel-customization/bundlers.md`  
> Upstream SHA: `2ccec778810094b582c21168e44fba6eec605f0a`

**Original:** Supported JavaScript bundlers influence builds and development flow.

**中文译文:** Admin panel 使用的 JavaScript bundler 会影响 development server、build 流程和扩展配置方式。

**Original:** Strapi's admin panel is a React-based SPA. Strapi 5 supports Vite (default) and webpack.

**中文译文:** Strapi admin panel 是 React-based single-page application。Strapi 5 支持两种 bundler：
- **Vite**：默认；
- **webpack**：可选。

**Original:** Documentation examples mention `strapi develop`, though you will commonly use `yarn develop` or `npm run develop`.

**中文译文:** 文档统一使用 `strapi develop` 表达 CLI command；实际项目通常通过 package manager alias 运行 `yarn develop` 或 `npm run develop`。

## Vite

**Original:** Vite is the default bundler used when running `strapi develop`.

**中文译文:** Strapi 5 默认使用 Vite build admin panel，因此普通 `strapi develop` 会自动使用 Vite。

**Original:** Extend Vite configuration in `/src/admin/vite.config` and always return the modified config.

**中文译文:** 如需扩展 Vite，在 `/src/admin/vite.config.js|ts` export 一个 config transformer，并**始终返回修改后的 config**。

**Original code (kept unchanged):**

```js title="/src/admin/vite.config.js"
const { mergeConfig } = require("vite");

module.exports = (config) => {
  return mergeConfig(config, {
    resolve: {
      alias: {
        "@": "/src",
      },
    },
  });
};
```

```ts title="/src/admin/vite.config.ts"
import { mergeConfig } from "vite";

export default (config) => {
  return mergeConfig(config, {
    resolve: {
      alias: {
        "@": "/src",
      },
    },
  });
};
```

**中文译文:** 示例使用 Vite `mergeConfig()` 增加 `@` alias。代码保持原样。

**Original:** Strapi also supports `vite.config.mts` for projects using explicit ESM module resolution.

**中文译文:** 对在 `package.json` 中显式使用 ESM module resolution 的项目，Strapi 还支持 `vite.config.mts`。这也有助于适应 Vite 6 开始 deprecated 的 CJS Node API。

## Webpack

**Original:** To use webpack instead of Vite, run:

`strapi develop --bundler=webpack`

**中文译文:** 若要切换到 webpack，运行：

`strapi develop --bundler=webpack`

**Original:** For webpack customization, rename the example config file in the project root to `webpack.config.js` or `webpack.config.ts`.

**中文译文:** 如果还要自定义 webpack，请把 project root 中的：
- `webpack.config.example.js` → `webpack.config.js`
- 或 `webpack.config.example.ts` → `webpack.config.ts`

Strapi 在 `--bundler=webpack` 模式下会自动读取该配置。

**Original code (kept unchanged):**

```js title="/src/admin/webpack.config.js"
module.exports = (config, webpack) => {
  config.plugins.push(new webpack.IgnorePlugin(/\/__tests__\//));
  return config;
};
```

```ts title="/src/admin/webpack.config.ts"
export default (config, webpack) => {
  config.plugins.push(new webpack.IgnorePlugin(/\/__tests__\//));
  return config;
};
```

**中文译文:** Strapi 会把 `webpack` instance 作为第二个 argument 传入，因此无需自行 `require('webpack')`。修改完成后必须 return config。
