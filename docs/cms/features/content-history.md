# 📖 对照翻译：Content History

> Source: `docusaurus/docs/cms/features/content-history.md`  
> Upstream SHA: `85073bf75cfa2eacc7b1ffa7a951c1a45baa7a6e`

**Original:** Content History stores previous document versions so editors can compare and restore earlier states from the Content Manager. Versions are only created for content edited in the Content Manager, and are kept for 14 days on the Growth plan and 30 days on the Enterprise plan.

**中文译文:** Content History 会保存 document 的历史版本，方便 editor 在 Content Manager 中查看并恢复到之前的状态。只有通过 Content Manager 修改的内容才会生成 version；Growth plan 默认保留 14 天，Enterprise plan 默认保留 30 天。

**Original:** The Content History feature, in the Content Manager, gives you the ability to browse and restore previous versions of documents created with the Content Manager.

**中文译文:** Content Manager 中的 Content History 功能可以浏览并恢复通过 Content Manager 创建的 document 历史版本。

**Original:** Plan: CMS Growth or Enterprise plan. Role & permission: None. Activation: Available by default if required plan. Environment: Development & Production.

**中文译文:** 功能属性：需要 CMS Growth 或 Enterprise plan；无额外 role/permission 要求；满足方案条件时默认可用；Development 与 Production environment 均支持。

**Original:** A version is only created when a document is modified through the Content Manager in the admin panel. Content modified in any other way does not appear in Content History, including REST API, GraphQL API, Document Service API, lifecycle hooks, cron jobs, and the `strapi import` and `strapi transfer` commands.

**中文译文:** 只有通过 admin panel 中 Content Manager 修改 document 时才会创建 version。通过其他方式修改的内容不会出现在 Content History 中，包括 REST API、GraphQL API、Document Service API、lifecycle hooks、cron jobs，以及 `strapi import` 和 `strapi transfer` commands。

**Original:** Content History is not a record of every change. Programmatically written documents can differ from the most recent version listed in Content History. To trace admin-panel user actions, use Audit Logs.

**中文译文:** Content History 并不是每一次 document change 的完整审计记录。通过 migration script、REST API integration 等程序化方式写入的 document 不会有对应 version，因此 document 当前状态可能与 Content History 中最新 version 不同。若要追踪 admin panel 用户操作，请使用 [Audit Logs](/cms/features/audit-logs)。

## Configuration

**Original:** The only configurable aspect is how long versions are kept before deletion. A job runs once a day at midnight and deletes versions older than the retention period, counted from each version's creation date.

**中文译文:** 唯一可配置项是 version retention period。系统每天午夜运行一次 job，并根据每个 version 的 creation date 删除超过 retention period 的历史版本。

**Original:** Retention periods:

| Plan | Default retention period | Maximum retention period |
|---|---:|---:|
| CMS Growth | 14 days | 14 days |
| CMS Enterprise | 30 days | 90 days |

**中文译文:** Retention period：

| Plan | 默认保留时间 | 最大保留时间 |
|---|---:|---:|
| CMS Growth | 14 天 | 14 天 |
| CMS Enterprise | 30 天 | 90 天 |

**Original:** The retention period cannot be extended on Growth. Enterprise defaults to 30 days and can be extended to 90 days. Growth projects already using 30-day retention when the 14-day default was introduced keep it.

**中文译文:** Growth plan 的 retention period 不能延长。Enterprise 默认 30 天，最多可延长到 90 天。14 天默认值引入前已经使用 30 天 retention 的 Growth projects 会继续保留该设置。

**Original:** Versions deleted by the retention job cannot be recovered from the Content History interface.

**中文译文:** 被 retention job 删除的 versions 无法从 Content History 界面恢复。

### Code-based configuration

**Original:** The retention period can be shortened, but never extended, with `history.retentionDays` in `/config/admin`. When both the license and configuration define a value, the lower one applies.

**中文译文:** 可以通过 `/config/admin` 中的 `history.retentionDays` 缩短 retention period，但不能延长。License 与配置文件都定义值时，使用较小值。

**Original code (kept unchanged):**

```js title="/config/admin.js"
module.exports = ({ env }) => ({
  // … other configuration properties
  history: {
    retentionDays: 7,
  },
});
```

```ts title="/config/admin.ts"
export default ({ env }) => ({
  // … other configuration properties
  history: {
    retentionDays: 7,
  },
});
```

**中文译文:** 示例将 retention period 缩短为 7 天。代码保持原样。Admin panel 中没有等价设置。

## Usage

**Original:** Path: Content Manager. From the edit view of a content type, click the top-right menu and then Content History.

**中文译文:** 使用路径：*Content Manager*。在 content type 的 edit view 中，点击右上角菜单，然后选择 **Content History**。

### Browsing Content History

**Original:** The main view on the left lists fields and content for the selected version. The sidebar on the right shows the total number of versions and, for each version, creation date/time, user, and whether status is Draft, Modified, or Published.

**中文译文:** 左侧 main view 展示当前选中 version 的 fields 与内容；右侧 sidebar 显示可用 versions 总数，并对每个 version 显示 creation date/time、创建者，以及 Draft、Modified 或 Published 状态。

**Original:** The main view clearly states whether a field was inexistent, deleted, or renamed in other versions. Fields unknown for the selected version appear under an Unknown fields heading.

**中文译文:** Main view 会明确说明 field 在其他 version 中是否不存在、被删除或重命名。对于当前所选 version 无法识别的 fields，会显示在 *Unknown fields* 标题下。

### Restoring a previous version

**Original:** Restoring a version overrides the current draft content with the selected version. The document switches to Modified status and can then be published whenever you want.

**中文译文:** Restore 某个 version 时，该 version 内容会覆盖当前 draft 内容。Document 会切换到 Modified 状态，之后可以按需要重新 publish。

**Original:** 1. Browse Content History and select a version.
2. Click **Restore**.
3. Confirm with **Restore**.

**中文译文:** 1. 浏览 Content History，并在右侧 sidebar 选择目标 version；
2. 点击 **Restore**；
3. 在 confirmation 窗口再次点击 **Restore**。

**Original:** If i18n is enabled, restoring a version with a unique field restores that field's content for all locales.

**中文译文:** 如果 content-type 启用了 [Internationalization (i18n)](/cms/features/internationalization)，restore 包含 unique field 的 version 时，该 field 的内容会对所有 locales 一并恢复。
