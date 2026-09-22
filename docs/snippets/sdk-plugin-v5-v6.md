# 📖 对照翻译：Using Plugin SDK v5

> Source: `docusaurus/docs/snippets/sdk-plugin-v5-v6.md`  
> Upstream SHA: `78930ad86c2724d281f52a5ce56385595187d1bf`

**Original:** Pin `@strapi/sdk-plugin@5` only if you need the legacy `@strapi/pack-up` build system and `packup.config.ts`.

**中文译文:** 只有在必须继续使用旧 `@strapi/pack-up` build system 与 `packup.config.ts` 时才建议固定 Plugin SDK v5：

```bash
# Yarn
yarn add @strapi/sdk-plugin@5

# NPM
npm install @strapi/sdk-plugin@5
```

**Original:** v6 is recommended for security updates and simpler configuration.

**中文译文:** 新 plugin 应使用 SDK v6，以获得安全更新，并通过 `package.json#exports` 自动推导 build config。
