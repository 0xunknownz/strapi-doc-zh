# 📖 对照翻译：Adding TypeScript support to existing Strapi projects

> Source: `docusaurus/docs/cms/typescript/adding-support-to-existing-project.md`  
> Upstream SHA: `25902e2323de8944d84f5290b76fb4f7e5a3f6aa`

**Original:** Add TypeScript support to an existing project by creating root/admin `tsconfig.json` files with `allowJs: true`, then rebuild the admin panel.

**中文译文:** 给现有 JavaScript Strapi 项目增加 TypeScript 支持时，需要创建 server 与 admin 两份 `tsconfig.json`。根配置中设置 `allowJs: true`，即可让 `.js` 与 `.ts/.tsx` 文件共存，实现渐进迁移。

## 1. Root `tsconfig.json`

**Original code (kept unchanged):**

```json title="./tsconfig.json"
{
  "extends": "@strapi/typescript-utils/tsconfigs/server",
  "compilerOptions": {
    "outDir": "dist",
    "rootDir": ".",
    "allowJs": true
  },
  "include": [
    "./",
    "src/**/*.json"
  ],
  "exclude": [
    "node_modules/",
    "build/",
    "dist/",
    ".cache/",
    ".tmp/",
    "src/admin/",
    "**/*.test.ts",
    "src/plugins/**"
  ]
}
```

**中文译文:** `allowJs: true` 是增量迁移的关键；`dist` 用作 TypeScript server code 的 compiled output。

## 2. Admin `tsconfig.json`

```json title="./src/admin/tsconfig.json"
{
  "extends": "@strapi/typescript-utils/tsconfigs/admin",
  "include": [
    "../plugins/**/admin/src/**/*",
    "./"
  ],
  "exclude": [
    "node_modules/",
    "build/",
    "dist/",
    "**/*.test.ts"
  ]
}
```

**中文译文:** Admin panel 使用独立 TypeScript configuration，并包含 local plugin admin source。

## 3. Optional ESLint cleanup

**Original:** Optionally delete old `.eslintrc` and `.eslintignore` files.

**中文译文:** 如果项目已有旧 ESLint setup，可根据当前 lint strategy 选择移除旧 `.eslintrc` / `.eslintignore`。

## 4. SQLite path adjustment

**Original:** SQLite projects need an extra `..` in `database.ts` because compiled code runs from `dist`.

**中文译文:** SQLite 项目在迁移 TypeScript 后，compiled server code 位于 `dist`，因此 `database.ts` 中 database file path 通常要额外向上一级。

```js title="./config/database.ts"
const path = require('path');

module.exports = ({ env }) => ({
  connection: {
    client: 'sqlite',
    connection: {
      filename: path.join(
        __dirname,
        "..",
        "..",
        env("DATABASE_FILENAME", ".tmp/data.db")
      ),
    },
    useNullAsDefault: true,
  },
});
```

## 5. Rebuild

```bash
# Yarn
yarn build
yarn develop

# NPM
npm run build
npm run develop
```

**中文译文:** Build 后 project root 会生成 `dist` directory，并获得与新 TypeScript Strapi project 相同的 TypeScript development 能力。
