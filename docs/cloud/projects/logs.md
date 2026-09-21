# 📖 对照翻译：Cloud project logs

> Source: `docusaurus/docs/cloud/projects/logs.md`  
> Upstream SHA: `8af0b05608cd982d511f3b75f7850e80f03a305b`

**Original:** Cloud project logs

**中文译文:** Cloud 项目日志

**Original:** The Logs tab streams your project's live logs in a searchable, filterable table. Click any entry to inspect its full message and metadata.

**中文译文:** *Logs* 标签页会以可搜索、可筛选的表格形式实时展示项目日志。点击任意日志条目，可以查看完整消息及其 metadata。

**Original:** From the project dashboard, the *Logs* tab streams the live logs of the project as structured entries you can search, filter, and inspect.

**中文译文:** 在项目 dashboard 中，*Logs* 标签页会以结构化条目的形式实时展示项目日志，并支持搜索、筛选和详细查看。

**Original:** The *Logs* page is only accessible once the project has a successful deployment and is inaccessible during major environment operations, such as project creation, data transfer, or environment clearing.

**中文译文:** 只有项目至少成功完成一次 deployment 后，才能访问 *Logs* 页面。在执行重要 environment 操作时，例如创建项目、数据传输或清空 environment，该页面暂时不可用。

## Viewing logs

**Original:** The viewer follows the live logs stream and auto-scrolls to keep the latest entries in view. Each row shows three columns:

| Column | Description |
| --- | --- |
| Timestamp | When the log was emitted. |
| Type | The log level, *Error*, *Warning*, *Info*, or *HTTP*, shown as a colored badge. For *HTTP* entries, the response status code is shown next to the badge. |
| Message | The log message. Long messages are truncated in the table; click the entry to read the full text in the drawer. |

**中文译文:** Log viewer 会跟随实时日志流，并自动滚动以持续显示最新条目。每一行包含 3 列：

| 列 | 说明 |
| --- | --- |
| Timestamp | 日志产生时间。 |
| Type | 日志级别，包括 *Error*、*Warning*、*Info* 或 *HTTP*，并以不同颜色的 badge 显示。对于 *HTTP* 条目，badge 旁还会显示 response status code。 |
| Message | 日志消息。较长消息会在表格中截断；点击条目可在 drawer 中查看完整内容。 |

**Original:** You can copy a single log line by clicking the copy button visible on row hover, or within the drawer. To copy every entry currently shown in the log viewer, use the copy button in the toolbar instead.

**中文译文:** 将鼠标悬停到某行时，可以点击 copy 按钮复制单条日志；也可以在 drawer 中复制。若要复制当前 log viewer 中显示的全部条目，请使用 toolbar 中的 copy 按钮。

**Original:** The live log stream is currently limited to the last 15 minutes and capped at 100,000 rows. Historical log visibility is under development.

**中文译文:** 当前 live log stream 仅覆盖最近 15 分钟，并且最多显示 100,000 行。更完整的历史日志可见性仍在开发中。

## Inspecting a log entry

**Original:** Click any log row to open a detail drawer and display the full message and, when available, the *Metadata* of the log. The *Metadata* section shows the following information:

| Field | Description |
| --- | --- |
| `method` | HTTP method (e.g. `GET`, `POST`). |
| `path` | Requested path. |
| `route` | Matched application route. |
| `status_code` | HTTP response status code. |
| `error_type` | Error classification, when the entry is an error. |
| `duration_ms` | Time taken to handle the request, in milliseconds. |
| `response_size` | Size of the response. |
| `request_type` | Type of request (e.g. API, admin). |

**中文译文:** 点击任意日志行，会打开 detail drawer，并显示完整消息以及可用时的日志 *Metadata*。*Metadata* 区域包含以下信息：

| 字段 | 说明 |
| --- | --- |
| `method` | HTTP method，例如 `GET`、`POST`。 |
| `path` | 请求的 path。 |
| `route` | 匹配到的 application route。 |
| `status_code` | HTTP response status code。 |
| `error_type` | 当日志为错误时，对应的错误分类。 |
| `duration_ms` | 请求处理耗时，单位为毫秒。 |
| `response_size` | Response 大小。 |
| `request_type` | 请求类型，例如 API、admin。 |

## Viewing historical logs

**Original:** Use the timeframe selector in the toolbar to switch between live mode and a bounded historical range. The viewer defaults to the last 15 minutes.

**中文译文:** 使用 toolbar 中的 timeframe selector，可以在 live mode 与指定的历史时间范围之间切换。Log viewer 默认显示最近 15 分钟。

**Original:** Available time ranges depend on your Strapi Cloud plan:

| Time range | Plan availability |
| --- | --- |
| 15m, 1h, 4h, 24h, 2d, 7d | All plans |
| 14d | Pro / Business |
| 30d | Business |

**中文译文:** 可用时间范围取决于 Strapi Cloud 方案：

| 时间范围 | 可用方案 |
| --- | --- |
| 15m、1h、4h、24h、2d、7d | 所有方案 |
| 14d | Pro / Business |
| 30d | Business |

**Original:** For all non-live timeframes, a Refresh button appears next to the picker to manually reload the range. In live mode, logs refresh happens automatically.

**中文译文:** 选择非 live 的时间范围时，picker 旁会显示 **Refresh**，用于手动重新加载当前范围。在 live mode 下，日志会自动刷新。

## Searching and filtering logs

**Original:** You can use the search and filter tools to refine the logs displayed in the viewer. Filters and search combine, so you can, for example, show only *HTTP* entries with a *5xx* status that mention a specific route.

**中文译文:** 可以使用搜索和筛选工具进一步缩小 log viewer 中显示的日志范围。搜索条件与 filter 可以叠加，例如只显示状态为 *5xx*、且消息中包含特定 route 的 *HTTP* 条目。

**Original:** Projects deployed before the structured viewer was introduced display their logs as plain text, without search, filtering, or per-entry metadata. To access the new log viewer, trigger a manual redeployment of the project.

**中文译文:** 在结构化 log viewer 推出之前就已经部署的项目，其日志仍以纯文本显示，不支持搜索、筛选或单条日志 metadata。若要使用新的 log viewer，请手动重新部署一次项目。

### Search bar

**Original:** Type in the search field to keep only the entries whose message contains your text.

**中文译文:** 在搜索框中输入文本，只保留 message 中包含该文本的日志条目。

### Type filter

**Original:** Filter by the following log levels:

- Error
- Warning
- Info
- HTTP

Error logs are highlighted in red so they stand out as you scan.

**中文译文:** 可以按以下日志级别筛选：

- Error
- Warning
- Info
- HTTP

Error 日志会以红色高亮，方便快速识别。

### HTTP status code filter

**Original:** Filter by the following status codes:

- 2xx
- 3xx
- 4xx
- 5xx

**中文译文:** 可以按以下 HTTP status code 范围筛选：

- 2xx
- 3xx
- 4xx
- 5xx
