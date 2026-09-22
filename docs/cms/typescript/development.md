# 📖 对照翻译：TypeScript development with Strapi

> Source: `docusaurus/docs/cms/typescript/development.md`  
> Upstream SHA: `dad7ea421bf22d79f371b57a32aa6eabb9375d8a`

**Original:** TypeScript development includes Strapi typings, schema type generation, programmatic startup, and plugin-specific workflows.

**中文译文:** Strapi 的 TypeScript development 主要包括：
- 使用 `Core.Strapi` typings；
- 根据 content-type schema 自动生成 types；
- Programmatic startup；
- TypeScript plugin development。

## Use Strapi typings

**Original:** Import `Core` from `@strapi/strapi` and type the `strapi` argument.

```ts title="./src/index.ts"
import type { Core } from '@strapi/strapi';

export default {
  register({ strapi }: { strapi: Core.Strapi }) {
    // ...
  },
};
```

**中文译文:** 为 `strapi` instance 标注 `Core.Strapi` 后，IDE 可提供 properties、methods 与 lifecycle names 的 autocomplete。

## Generate typings from schemas

**Original:** Use `ts:generate-types`.

```bash
# NPM
npm run strapi ts:generate-types --debug

# Yarn
yarn strapi ts:generate-types --debug
```

**中文译文:** Command 会在 project root 创建 `types` directory，保存基于当前 schemas 生成的 typings。`--debug` 会输出更详细的 schema generation table。

**Original:** Automatic generation can be enabled with `autogenerate: true` in `config/typescript.js|ts`.

**中文译文:** 如果希望 server restart 时自动更新 types，可在 `config/typescript.js|ts` 设置：

`autogenerate: true`

## Generated types and build issues

**Original:** Generated types can be excluded from TypeScript compilation by adding `types/generated/**` to `tsconfig.json`.

**中文译文:** 如果 generated types 导致 build / Entity Service type-checking 问题，可以在 `tsconfig.json` 的 `exclude` 中加入：

`types/generated/**`

**Original:** Import public types from `@strapi/strapi`, not `@strapi/types`.

**中文译文:** **不要依赖 `@strapi/types` 作为公共 API。** 官方建议只从 `@strapi/strapi` import types，因为 `@strapi/types` 属于内部实现，可能无通知变更。

## Start Strapi programmatically

### `createStrapi()`

**Original:** TypeScript projects need `distDir`.

```js title="./server.js"
const strapi = require('@strapi/strapi');

const app = strapi.createStrapi({
  distDir: './dist',
});

app.start();
```

**中文译文:** Programmatic startup 时必须告诉 Strapi compiled code 在哪里，否则它无法加载 TypeScript project 的 build output。

### `strapi.compile()`

**Original:** `compile()` detects project language and returns the application context.

```js
const strapi = require('@strapi/strapi');

strapi
  .compile()
  .then((appContext) => strapi(appContext).start());
```

**中文译文:** `strapi.compile()` 更适合开发 tooling：它会自动检测项目是否含 TypeScript，必要时执行 compilation，再返回 Strapi startup 需要的 context。

## Plugin development

**Original:** Generate a plugin with TypeScript selected, install dependencies in the plugin directory, and rebuild after admin-side changes.

**中文译文:** TypeScript plugin 开发时：
1. 使用 plugin generator 并选择 TypeScript；
2. 在 plugin directory 中执行一次 `yarn` / `npm install`；
3. Admin-side code 变化后在 plugin directory 重新执行 `yarn build` / `npm run build`。

Dependency installation 通常只需首次执行；admin panel 相关 plugin 变更则需要重新 build。
