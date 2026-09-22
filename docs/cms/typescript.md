# 📖 对照翻译：TypeScript

> Source: `docusaurus/docs/cms/typescript.md`  
> Upstream SHA: `3e81e29c6f99eed0230a9d3437f47c3f9c4353e7`

**Original:** TypeScript adds a type system layer to Strapi applications, enabling type-safe code and automatic type generation.

**中文译文:** TypeScript 在 JavaScript 之上增加类型系统，使 Strapi application 获得更强的 type safety、自动类型生成与 IDE autocomplete。

**Original:** Any valid JavaScript is also valid TypeScript.

**中文译文:** 由于 TypeScript 是 JavaScript 的超集，合法 JavaScript 通常也是合法 TypeScript，因此可以渐进式迁移。

## Getting started

**Original:** Create a new TypeScript project with the `--typescript` flag.

```bash
# Yarn
yarn create strapi-app my-project --typescript

# NPM
npx create-strapi-app@latest my-project --typescript
```

**中文译文:** 新项目可以在创建时直接启用 TypeScript。命令保持原样。

**Original:** Existing JavaScript projects can add TypeScript support incrementally.

**中文译文:** 已有 JavaScript Strapi 项目可以按照 [Adding TypeScript support](/cms/typescript/adding-support-to-existing-project) 指南逐步迁移，而不需要一次性重写全部文件。

## What to do next

**Original:** Learn project structure, TypeScript configuration, development features, and guides.

**中文译文:** 推荐继续阅读：
- [Project structure](/cms/project-structure)
- [TypeScript configuration](/cms/configurations/typescript)
- [TypeScript development](/cms/typescript/development)
- [TypeScript guides](/cms/typescript/guides)
