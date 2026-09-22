# 📖 对照翻译：AI for content managers

> Source: `docusaurus/docs/cms/ai/for-content-managers.md`  
> Upstream SHA: `53489e2557af87fe3526412067e435f4a9de856b`

**Original:** Strapi AI helps content managers design content structures, translate content, and generate asset metadata from the admin panel. Strapi also includes a built-in MCP server that lets AI clients manage content through natural language.

**中文译文:** Strapi AI 面向 content manager 提供 admin-panel 内置 AI 能力，包括辅助设计 content structure、自动翻译内容、生成 media metadata；同时 Strapi 还提供 built-in MCP server，让外部 AI client 能通过自然语言管理内容。

## Strapi AI availability

**Original:** Strapi AI is available on Growth plans since Strapi 5.30 for Cloud and self-hosted deployments.

**中文译文:** Strapi AI 从 Strapi 5.30 起面向 Growth plan 提供，Strapi Cloud 与 self-hosted deployment 均可使用。

**Original:** Requirements:
1. Strapi 5.30+
2. Growth license or 30-day trial
3. AI features are enabled by default in supported admin areas

**中文译文:** 启用条件：
1. 升级到 Strapi 5.30+；
2. 使用 Growth license，或启动 30-day free trial；
3. Content-Type Builder、Media Library、Content Manager 中的 AI capability 默认开启。

## Global configuration

```js title="/config/admin.js|ts"
module.exports = {
  ai: {
    enabled: true,
  },
};
```

**中文译文:** 设置 `ai.enabled: false` 可以全局关闭 Strapi AI features。

## Available features

| Feature | 中文说明 |
|---|---|
| Content-Type Builder AI | 使用 chat assistant 设计 content types、解释 schema、规划 data model，并利用现有 schemas 作为 context |
| Internationalization AI | 保存 entry 时，将 default locale content 自动翻译到其他 locales |
| Media Library AI | 为上传 image 生成 alternative text、caption 与 description |

## Credits

**Original:** Growth includes 1,000 AI credits per month; free trial includes 10 credits. Enterprise plans do not include Strapi AI.

**中文译文:** Strapi AI credits：
- Growth plan：每月 1,000 credits；
- Free trial：10 credits；
- Enterprise plan 当前不提供 Strapi AI。

**Original:** Complex actions consume more credits. Usage is visible in Settings Overview; notifications are sent at 80%, 90%, and 100%. Overage billing applies.

**中文译文:** 不同 AI action 消耗 credits 不同，复杂任务消耗更多。Admin panel 的 Settings Overview 可查看 usage；达到 80%、90%、100% 时会收到通知。超过 monthly allowance 后可以继续使用，并按月收取 overage。

**Original:** Credits are shared across all users in the same project instance.

**中文译文:** 同一 project instance 中的所有 users 共用同一份 AI credits。

**Original:** AI requests are processed through Strapi-managed infrastructure; content is used temporarily and not stored outside the instance.

**中文译文:** AI request 通过 Strapi-managed infrastructure 处理；content 仅在 request 过程中临时使用，不作为持久内容存储在 instance 之外。Strapi 表示其数据处理遵循与 Strapi Cloud 相同的 GDPR-aligned framework。

## Strapi MCP server

**Original:** The built-in Strapi MCP server lets MCP-compatible AI clients create, read, update, delete, publish, and unpublish content through Content Manager, gated by Admin token permissions.

**中文译文:** Built-in Strapi MCP server 可以让 Claude、Cursor 等 MCP-compatible AI client 通过自然语言：
- Create
- Read
- Update
- Delete
- Publish
- Unpublish

Content operations 仍受 Admin token permissions 限制。
