# 📖 对照翻译：Media Library provider notes

> Source: `docusaurus/docs/snippets/media-library-providers-notes.md`  
> Upstream SHA: `46bfca5832d2a3c258185c2db73d763864ec14df`

**Original:** Strapi's default security middleware has a strict Content Security Policy that limits images and media to `'self'`.

**中文译文:** Strapi 默认 security middleware 使用严格 Content Security Policy，image / media 默认只允许从 `'self'` 加载。使用外部 storage provider 时，应按 provider domain 调整 CSP。

**Original:** Configure different providers per environment under `/config/env/<environment>/plugins.js|ts`.

**中文译文:** 若不同 environment 使用不同 Media Library provider，应在 `/config/env/<environment>/plugins.js|ts` 中分别配置。
