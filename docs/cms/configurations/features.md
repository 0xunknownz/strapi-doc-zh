# 📖 对照翻译：Features configuration

> Source: `docusaurus/docs/cms/configurations/features.md`  
> Upstream SHA: `708b6bfb324131154b251d0636fbfad0f899b930`

**Original:** Future flags in `/config/features` toggle experimental Strapi features, allowing early testing at your own risk.

**中文译文:** `config/features.js|ts` 用于控制 Strapi feature flags。**Future flags** 用于提前启用 experimental feature；**stable flags** 则切换已经正式发布功能的行为。

**Original:** Future flags are nested in a `future` object; stable flags live at the top level.

**中文译文:**
- Future flag：放在 `future: { ... }` 内；
- Stable flag：直接放在 `config/features` 顶层。

**Original:** Experimental features can change, be removed, contain breaking changes, or be incomplete.

**中文译文:** Future flags 应谨慎用于 production。Experimental feature 可能：
- 行为或 API 发生变化；
- 被删除；
- 包含 breaking change；
- 尚未稳定或部分仍使用 mock / unfinished implementation。

## Enabling a future flag

**Original:** Add the flag under `future`, optionally reading it from an environment variable.

**中文译文:** 启用 future flag 时，在 `future` object 中加入对应 property，并通常通过 environment variable 控制。

**Original code (kept unchanged):**

```js title="/config/features.js"
module.exports = ({ env }) => ({
  future: {
    experimental_firstPublishedAt: env.bool(
      'STRAPI_FUTURE_EXPERIMENTAL_FIRST_PUBLISHED_AT',
      false
    ),
  },
});
```

```dotenv title=".env"
STRAPI_FUTURE_EXPERIMENTAL_FIRST_PUBLISHED_AT=true
```

**中文译文:** 如果环境变量不存在，则 `env.bool(..., false)` 会让 feature 保持 disabled。修改后需要重新启动 / rebuild admin。

## Future flags API

**Original:** Feature configuration is accessible through `strapi.config.get('features')` or `strapi.features.config`.

**中文译文:** Runtime 中可以通过：
- `strapi.config.get('features')`
- `strapi.features.config`
读取 feature configuration。

**Original:** Check a future flag with `strapi.features.future.isEnabled('featureName')`.

**中文译文:** 判断 future flag 是否启用：

`strapi.features.future.isEnabled('featureName')`

**Original:** Check a stable flag with `strapi.features.isEnabled('flagName')`.

**中文译文:** Stable flag 使用：

`strapi.features.isEnabled('flagName')`

## Available future flag

**Original:** `experimental_firstPublishedAt` enables first-publication-date recording for Draft & Publish.

**中文译文:** 当前列出的 future flag：
- `experimental_firstPublishedAt`：为 Draft & Publish 启用 first publication date 记录；
- 推荐 environment variable：`STRAPI_FUTURE_EXPERIMENTAL_FIRST_PUBLISHED_AT`。

## Stable flag

**Original:** `useLegacyMediaLibrary` restores the previous Media Library interface. Default is `false`.

**中文译文:** Stable flag `useLegacyMediaLibrary` 可以恢复旧版 Media Library UI。默认 `false`，即使用 redesigned interface。

```js title="/config/features.js"
module.exports = ({ env }) => ({
  useLegacyMediaLibrary: env.bool('USE_LEGACY_MEDIA_LIBRARY', false),
});
```
