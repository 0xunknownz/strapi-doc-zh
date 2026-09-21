# 📖 对照翻译：Audit Logs

> Source: `docusaurus/docs/cms/features/audit-logs.md`  
> Upstream SHA: `5bcda195cc5a913df75d79aec8873592f88a0a91`

**Original:** Audit Logs captures every administrative action in a searchable, filterable history to aid troubleshooting and compliance. In this documentation, examples show viewing payloads and filtering by user or date.

**中文译文:** Audit Logs 会把 administrative actions 记录到可搜索、可筛选的历史日志中，帮助进行故障排查与合规审计。本页介绍如何查看 payload，并按 user 或 date 筛选日志。

**Original:** The Audit Logs feature provides a searchable and filterable display of all activities performed by users of the Strapi application.

**中文译文:** Audit Logs 功能以可搜索、可筛选的形式展示 Strapi application 用户执行的全部活动。

**Original:** Plan: CMS Enterprise plan. Role & permission: Super Admin role. Activation: Available by default if required plan. Environment: Available in Development & Production.

**中文译文:** 功能属性：需要 CMS Enterprise plan；默认面向项目 admin panel 中的 Super Admin role；满足方案条件时默认可用；Development 与 Production environment 均支持。

## Configuration

**Original:** The only configurable aspect is how long logs are kept before they are deleted. Audit Logs are not a permanent archive. Logs older than the retention period are deleted automatically. The retention period defaults to 90 days.

**中文译文:** Audit Logs 唯一可配置项是日志 retention period。Audit Logs 不是永久 archive；超过 retention period 的日志会自动删除。默认 retention period 为 90 天。

**Original:** Logs deleted at the end of the retention period cannot be recovered from the Audit Logs interface.

**中文译文:** Retention period 到期后被删除的日志，无法从 Audit Logs 界面恢复。

### Code-based configuration

**Original:** The retention period is set with the `auditLogs.retentionDays` parameter of the `/config/admin` file. For Strapi Cloud projects, the value stored in the license information applies unless a smaller value is defined in the configuration file.

**中文译文:** Retention period 通过 `/config/admin` 中的 `auditLogs.retentionDays` 设置。对于 Strapi Cloud 项目，默认采用 license 中记录的值；如果配置文件中设置了更小的值，则使用较小值。

**Original code (kept unchanged):**

```js title="/config/admin.js"
module.exports = ({ env }) => ({
  // … other configuration properties
  auditLogs: {
    retentionDays: 30,
  },
});
```

```ts title="/config/admin.ts"
export default ({ env }) => ({
  // … other configuration properties
  auditLogs: {
    retentionDays: 30,
  },
});
```

**中文译文:** 示例将 retention period 设置为 30 天。代码保持原样。

**Original:** There is no equivalent setting in the admin panel: the retention period can only be configured from the `/config/admin` file.

**中文译文:** Admin panel 中没有对应设置；retention period 只能通过 `/config/admin` 配置。

## Usage

**Original:** Path to use the feature: Settings > Administration Panel - Audit Logs.

**中文译文:** 使用路径：*Settings > Administration Panel - Audit Logs*。

**Original:** Audit Logs records these events:

| Event | Actions |
| --- | --- |
| Content Type | `create`, `update`, `delete` |
| Entry (draft/publish) | `create`, `update`, `delete`, `publish`, `unpublish` |
| Media | `create`, `update`, `delete` |
| Login / Logout | `success`, `fail` |
| Releases | `create`, `update`, `delete`, `trigger` |
| Release entries | `add`, `update`, `remove` |
| Release settings | `update` |
| Role / Permission | `create`, `update`, `delete` |
| User | `create`, `update`, `delete` |

**中文译文:** Audit Logs 会记录以下 events 与 actions：

| Event | Actions |
| --- | --- |
| Content Type | `create`、`update`、`delete` |
| Entry（draft/publish） | `create`、`update`、`delete`、`publish`、`unpublish` |
| Media | `create`、`update`、`delete` |
| Login / Logout | `success`、`fail` |
| Releases | `create`、`update`、`delete`、`trigger` |
| Release entries | `add`、`update`、`remove` |
| Release settings | `update` |
| Role / Permission | `create`、`update`、`delete` |
| User | `create`、`update`、`delete` |

**Original:** Each log item displays Action, Date, User, and Details. Details opens a modal with more information such as User IP address, request body, or response body.

**中文译文:** 每条日志显示 Action、Date、User 和 Details。Details 会打开 modal，展示更多信息，例如 User IP address、request body 或 response body。

**Original:** With Strapi 5.52.0+ logged actions can come from the admin panel or from the MCP server. Entry actions performed through the MCP server are logged like their admin panel equivalents. Actions that only read content are not logged.

**中文译文:** Strapi 5.52.0+ 中，记录的 actions 可以来自 admin panel 或 [MCP server](/cms/features/strapi-mcp-server)。通过 MCP server 执行的 entry actions 会像对应 admin panel 操作一样被记录；只读取内容的 actions 不会记录。

### Filtering logs

**Original:** By default, all logs are displayed in reverse chronological order. You can filter by Action, User, and Date.

**中文译文:** 默认情况下，所有 logs 按时间倒序显示。可以按 Action、User 和 Date（含日期范围与时间）筛选。

### Accessing log details

**Original:** Click the eye icon for a log item to open a modal with more details. The Payload section displays an interactive JSON component that can be expanded and collapsed.

**中文译文:** 点击某条日志的 eye 图标可以打开详情 modal。*Payload* 区域使用交互式 JSON component 展示详细信息，并支持展开和折叠 JSON object。

**Original:** With Strapi 5.52.0, the `origin` key in the payload indicates where the action came from: `mcp` for the MCP server or `admin` for the admin panel.

**中文译文:** Strapi 5.52.0 中，payload 的 `origin` key 用于标记 action 来源：`mcp` 表示 MCP server，`admin` 表示 admin panel。

### Exporting audit logs

**Original:** Users with the `export` permission for Audit Logs can export the current filtered set as a CSV file. The user's role needs both Read and Export permissions under Settings > Administration Panel > Roles > Audit Logs.

**中文译文:** 拥有 Audit Logs `export` permission 的用户可以把当前筛选结果导出为 CSV。对应 role 必须在 *Settings > Administration Panel > Roles > Audit Logs* 中同时具备 **Read** 和 **Export** permissions。

**Original:** To export audit logs:
1. Optionally apply filters.
2. Click **Export** to start pre-downloading. Keep the browser tab open.
3. Click **Download CSV** to save the file.

**中文译文:** 导出 audit logs：
1. （可选）先应用 filters；
2. 点击 **Export** 开始预下载，完成前保持 browser tab 打开；
3. 点击 **Download CSV** 保存文件。

**Original:** Every export is recorded as an `audit-log.export` event, and that event is included in the exported CSV file.

**中文译文:** 每次 export 本身都会被记录为 `audit-log.export` event，并包含在导出的 CSV 中。

**Original:** Exports are limited to 1,000,000 rows by default. Change the limit with `auditLogs.exportMaxRows`.

**中文译文:** Export 默认最多 1,000,000 rows。可通过 admin panel configuration 中的 `auditLogs.exportMaxRows` 修改上限。
