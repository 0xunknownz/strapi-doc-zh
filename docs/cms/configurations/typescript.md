# 📖 对照翻译：TypeScript configuration

> Source: `docusaurus/docs/cms/configurations/typescript.md`  
> Upstream SHA: `89d7b354199b04b695954110ad905de4c6bbb3b7`

**Original:** TypeScript configuration covers tsconfig files, output directories, and an optional `config/typescript.js|ts` that can auto-generate types on server restart.

**中文译文:** TypeScript-enabled Strapi project 通过 `tsconfig.json` 控制 compilation，并使用特定 output directories。还可以添加 `config/typescript.js|ts`，在 server restart 时自动生成 Strapi schema typings。

## Project structure

| TypeScript-specific path | 中文说明 |
|---|---|
| `./dist` | 编译后的 JavaScript 输出根目录 |
| `./dist/build` | Admin panel compiled JavaScript；首次 build 后生成 |
| `./tsconfig.json` | Server TypeScript compilation |
| `./src/admin/tsconfig.json` | Admin panel TypeScript compilation |

**Original:** Generated Strapi types are based on the user's project schema and improve autocompletion.

**中文译文:** Strapi 根据当前 project structure / content-type schemas 生成 type definitions，并读取这些 typings 来增强 editor autocomplete 和类型推断。

## Strapi-specific TypeScript configuration

**Original:** This feature is experimental.

**中文译文:** Strapi-specific automatic type generation configuration 当前属于 **Experimental**，可能存在兼容性问题或行为变化。

**Original:** `autogenerate` enables automatic type generation when the server restarts. Default: `false`.

**中文译文:** 当前唯一配置项：

| Parameter | Type | Default | 中文说明 |
|---|---|---|---|
| `autogenerate` | Boolean | `false` | Server restart 时自动重新生成 types |

**Original code (kept unchanged):**

```js title="./config/typescript.js"
module.exports = ({ env }) => ({
  autogenerate: true,
});
```

```ts title="./config/typescript.ts"
export default ({ env }) => ({
  autogenerate: true,
});
```

**中文译文:** 启用后无需每次 server restart 后手工运行 type-generation command。
