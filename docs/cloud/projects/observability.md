# 📖 对照翻译：Cloud project observability

> Source: `docusaurus/docs/cloud/projects/observability.md`  
> Upstream SHA: `8dc2685b34df319e58e74c47b398f10c47805404`

**Original:** Cloud project observability

**中文译文:** Cloud 项目可观测性

**Original:** The Observability tab surfaces usage metrics, endpoint traffic, and infrastructure health data directly from your project dashboard. Use it to monitor API and bandwidth consumption, identify high-traffic endpoints, and track CPU and Memory usage over time.

**中文译文:** *Observability* 标签页直接在项目 dashboard 中展示用量指标、endpoint 流量以及基础设施健康数据。你可以用它监控 API 与 bandwidth 消耗、识别高流量 endpoint，并持续跟踪 CPU 与 Memory 使用情况。

**Original:** The *Observability* tab is accessible from your project dashboard. It contains 4 sections: Summary, Project consumption, Traffic insights, and CPU and Memory usage.

**中文译文:** 可以从项目 dashboard 进入 *Observability* 标签页。页面包含 4 个区域：Summary、Project consumption、Traffic insights，以及 CPU and Memory usage。

## Summary

**Original:** The *Summary* section displays a monthly overview of your resource consumption and any overage charges.

**中文译文:** *Summary* 区域按月汇总资源消耗情况，并显示相应的 overage 费用。

**Original:** Use the month picker in the top-right corner of the section to view previous months.

**中文译文:** 使用区域右上角的 month picker 可以查看之前月份的数据。

**Original:** The section contains 4 metric cards:

| Card | Description |
|------|-------------|
| API requests | Total API requests for the month, shown against your plan limit with a progress bar. Displays overage charges if the limit was exceeded. |
| Asset bandwidth | Total bandwidth consumed for the month, shown against your plan limit with a progress bar. Displays overage charges if the limit was exceeded. |
| Asset storage | Storage used per environment. Each environment shows a progress bar with its usage against its limit. Displays overage charges if the limit was exceeded on any environment at any point throughout the month. |
| Overage charges | Total overage amount for the month, excluding applicable taxes. |

**中文译文:** 该区域包含 4 张 metric card：

| 卡片 | 说明 |
|------|-------------|
| API requests | 本月 API 请求总量，并通过 progress bar 与当前方案额度对比。如果超出上限，会显示 overage 费用。 |
| Asset bandwidth | 本月总 bandwidth 消耗，并通过 progress bar 与当前方案额度对比。如果超出上限，会显示 overage 费用。 |
| Asset storage | 按 environment 展示 storage 使用量。每个 environment 都会通过 progress bar 显示当前用量与上限的对比。如果当月任意时间某个 environment 超出上限，会显示 overage 费用。 |
| Overage charges | 本月 overage 总金额，不包含适用税费。 |

**Original:** API requests data is available in real time, whereas Asset bandwidth and Asset storage are updated hourly. To update these metrics, refresh the dashboard.

**中文译文:** API requests 数据实时更新；Asset bandwidth 和 Asset storage 则按小时更新。若要获取最新指标，请刷新 dashboard。

**Original:** For more information on usage billing and overage management, see Usage & Billing.

**中文译文:** 关于用量计费和 overage 管理的更多信息，请参阅 [Usage & Billing](/cloud/getting-started/usage-billing)。

## Project consumption

**Original:** The *Project consumption* section shows API requests and asset bandwidth usage over time, broken down by environment.

**中文译文:** *Project consumption* 区域按 environment 展示 API requests 与 Asset bandwidth 随时间变化的使用情况。

**Original:** Use the time range selector in the top-right corner to adjust the period displayed:

| Time range | Plan availability |
|------------|-------------------|
| 24h | All plans |
| 7d | All plans |
| 14d | Pro / Business |
| 30d | Pro / Business |
| 60d | Business |

**中文译文:** 使用右上角的 time range selector 可以调整显示时间范围：

| 时间范围 | 可用方案 |
|------------|-------------------|
| 24h | 所有方案 |
| 7d | 所有方案 |
| 14d | Pro / Business |
| 30d | Pro / Business |
| 60d | Business |

**Original:** The section contains 2 charts:

- API requests: total API calls across all environments, displayed as a stacked bar chart.
- Asset bandwidth: total data transferred for assets across all environments, using the same stacked bar format.

**中文译文:** 该区域包含 2 张图表：

- API requests：所有 environments 的 API calls 总量，以 stacked bar chart 展示；
- Asset bandwidth：所有 environments 的资源数据传输总量，同样使用 stacked bar chart 展示。

**Original:** Each bar represents a time bucket (hourly or daily, depending on the selected range) and is stacked by environment. Hover over the chart to see a tooltip showing the consumption breakdown per environment at a specific point in time. To filter out environments from the graph, click on their name in the legend.

**中文译文:** 每个 bar 代表一个时间 bucket（根据所选时间范围按小时或按天聚合），并按 environment 堆叠。将鼠标悬停在图表上，可以通过 tooltip 查看某个时间点各 environment 的用量明细。若要从图表中隐藏某个 environment，点击 legend 中对应名称即可。

## Traffic insights

**Original:** The *Traffic insights* section shows which API endpoints and assets generate the most traffic for the selected environment and time range.

**中文译文:** *Traffic insights* 区域会根据所选 environment 和时间范围，显示哪些 API endpoints 和 assets 产生了最多流量。

**Original:** Use the *environment* dropdown and the time range selector to filter the data. The available time ranges are the same as in Project consumption.

**中文译文:** 使用 *environment* 下拉菜单和 time range selector 可以筛选数据。可用时间范围与 [Project consumption](#project-consumption) 相同。

### Top endpoints by API traffic

**Original:** The *Top endpoints by API traffic* table lists the 5 API endpoints that received the most requests in the selected period and displays the following metrics:

| Column | Description |
|--------|-------------|
| Endpoint | The matched API route path. |
| Requests | Total number of requests in the selected period. |
| P50 (ms) | Median response time. 50% of requests completed faster than this value. |
| P95 (ms) | 95th percentile response time. 95% of requests completed faster than this value. |
| P99 (ms) | 99th percentile response time. 99% of requests completed faster than this value. |
| Max (ms) | The highest single response time recorded in the selected period. |
| Error rate (%) | Percentage of requests that returned a 4xx response. |

**中文译文:** *Top endpoints by API traffic* 表格列出所选时间段内请求量最高的 5 个 API endpoints，并显示以下指标：

| 列 | 说明 |
|--------|-------------|
| Endpoint | 匹配到的 API route path。 |
| Requests | 所选时间段内的请求总数。 |
| P50 (ms) | 响应时间中位数；50% 的请求完成时间低于该值。 |
| P95 (ms) | 响应时间第 95 百分位；95% 的请求完成时间低于该值。 |
| P99 (ms) | 响应时间第 99 百分位；99% 的请求完成时间低于该值。 |
| Max (ms) | 所选时间段内记录到的单次最高响应时间。 |
| Error rate (%) | 返回 4xx response 的请求占比。 |

### Top assets by bandwidth usage

**Original:** The *Top assets by bandwidth usage* table lists the 5 assets that consumed the most bandwidth in the selected period and displays the following metrics:

| Column | Description |
|--------|-------------|
| Asset path | The file path of the asset. |
| Total bandwidth | Total data transferred for this asset in the selected period. |

**中文译文:** *Top assets by bandwidth usage* 表格列出所选时间段内 bandwidth 消耗最高的 5 个 assets，并显示以下指标：

| 列 | 说明 |
|--------|-------------|
| Asset path | Asset 的文件路径。 |
| Total bandwidth | 所选时间段内该 asset 的总数据传输量。 |

## CPU and Memory usage

**Original:** The *CPU and Memory over time* section shows your application's CPU and Memory consumption as a percentage of the available resources.

**中文译文:** *CPU and Memory over time* 区域以可用资源百分比的形式展示应用 CPU 与 Memory 消耗。

**Original:** The section displays a single area chart with 2 series:

- CPU: displayed as a blue dashed line
- Memory: displayed as a green solid line

**中文译文:** 该区域包含一张 area chart，并显示 2 个 series：

- CPU：蓝色虚线；
- Memory：绿色实线。

**Original:** Use the *environment* dropdown at the top right of the view to select which environment's metrics to display and the time range selector to adjust the period. Hover over the chart to see a tooltip showing the CPU and Memory values at a specific point in time. Data is displayed hourly or daily, depending on the selected range.

**中文译文:** 使用视图右上角的 *environment* 下拉菜单选择要查看哪个 environment 的指标，并通过 time range selector 调整时间范围。将鼠标悬停在图表上，可以通过 tooltip 查看某一时间点的 CPU 与 Memory 数值。数据会根据所选时间范围按小时或按天展示。

**Original:** Click the refresh button in the section toolbar to manually load the latest data. The section also refreshes automatically:

- Every 30 seconds for the 5m and 15m ranges
- Every 5 minutes for the 1h, 24h and 7d ranges

**中文译文:** 点击区域 toolbar 中的 refresh 按钮，可以手动加载最新数据。该区域也会自动刷新：

- 选择 5m 或 15m 范围时，每 30 秒刷新一次；
- 选择 1h、24h 或 7d 范围时，每 5 分钟刷新一次。
