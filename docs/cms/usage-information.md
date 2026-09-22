# 📖 对照翻译：Collected Usage Information

> Source: `docusaurus/docs/cms/usage-information.md`  
> Upstream SHA: `98a1ea8c8da15d76ce965584a44ae45ddf1c54d8`

**Original:** Strapi collects non-sensitive aggregated data such as project ID, machine ID, environment state, and OS to improve the platform. Data collection follows GDPR guidance and can be disabled.

**中文译文:** Strapi 默认收集部分非敏感、聚合后的 usage data，例如 project ID、machine ID、environment state 与 OS，用于了解全局产品使用情况并改进 Strapi。官方声明该流程遵循 GDPR，并提供 opt-out。

## Why telemetry exists

**Original:** Aggregated usage data helps Strapi understand feature adoption, install time, common errors, plugin usage, and broader product behavior.

**中文译文:** Telemetry 主要用于回答产品层问题，例如：
- 哪些 features 被实际使用；
- Feature 是否常与某 plugin / environment 一起使用；
- Project setup 时间是否变长；
- 用户常遇到哪些 errors；
- 哪些 plugins 最常用。

**Original:** This complements surveys, UX testing, issue tracking, roadmap votes, and community feedback.

**中文译文:** Telemetry 并不是唯一 feedback channel，而是与 UX testing、survey、issue tracking、roadmap voting、community discussion 等信息共同使用。

## Collected data

**Original:** Strapi collects:
- unique project ID,
- unique machine ID,
- environment state,
- OS/system information,
- build configuration.

**中文译文:** Strapi 文档列出的 telemetry data 包括：
- Unique project ID（UUID）；
- Unique machine ID；
- Environment state（development / staging / production）；
- System / OS information；
- Build configuration。

**Original:** It does not collect database configuration, passwords, or custom variables.

**中文译文:** 官方明确表示不会收集：
- Database configuration；
- Password；
- Custom environment variables。

收集的数据会经过 secure transport、encryption 与 anonymization。

## Marketing opt-in

**Original:** If a user checks the marketing opt-in box during initial registration, email, first name, and company role are sent to the marketing team.

**中文译文:** 首次注册时，如果用户主动勾选“接收新功能和改进信息”，则 email、first name、company role 会发送给 marketing team，仅用于营销相关用途；这些信息不进入 telemetry system，而且默认不 opt-in。

## Opt out

**Original:** Do not disable telemetry by removing the project UUID.

**中文译文:** 过去曾建议删除 `package.json` 中的 `uuid`，但现在不推荐这样做，因为 UUID 可能被其他项目功能依赖，而且未来重新加入 UUID 会无提示恢复 telemetry。

**Original:** Use the CLI:

```bash
# Yarn
yarn strapi telemetry:disable

# NPM
npm run strapi telemetry:disable
```

**中文译文:** 推荐使用官方 CLI command 禁用 telemetry。

**Original:** You can also set `strapi.telemetryDisabled: true` in `package.json`.

**中文译文:** 也可以在 project `package.json` 中设置：

`strapi.telemetryDisabled: true`

**Original:** Re-enable by deleting the flag, setting it to false, or running `telemetry:enable`.

**中文译文:** 后续可通过删除 flag、改为 `false`，或运行 `telemetry:enable` 恢复。

## Strapi AI data handling

**Original:** Strapi AI requests are processed through Strapi-managed infrastructure. Temporary metadata/content snippets exist only for the duration of the request.

**中文译文:** Strapi AI request 通过 Strapi-managed infrastructure 处理。Temporary metadata 与 content snippets 只在单次 request 生命周期内存在。

**Original:** Strapi does not store unpublished content or credentials outside the instance.

**中文译文:** 官方声明不会在 Strapi instance 之外持久存储 unpublished content 或 credentials。

**Original:** AI processing follows the same GDPR-aligned framework as Strapi Cloud and data is not retained after the operation.

**中文译文:** Strapi AI 的数据处理采用与 Strapi Cloud 一致的 GDPR-aligned framework；operation 完成后不保留该 request 的内容数据。
