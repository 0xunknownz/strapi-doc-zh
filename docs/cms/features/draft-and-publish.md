# 📖 对照翻译：Draft & Publish

> Source: `docusaurus/docs/cms/features/draft-and-publish.md`  
> Upstream SHA: `769704932728797d17a842e9e482c028387fb874`

**Original:** Draft & Publish separates drafts from live entries, allowing editors to stage content before release. This documentation shows how to enable it per content type and manage publish or unpublish actions.

**中文译文:** Draft & Publish 将 draft 与线上已发布 entry 分离，让 editor 可以在正式发布前准备和修改内容。本页介绍如何按 content type 启用该功能，以及如何执行 publish / unpublish。

**Original:** The Draft & Publish feature allows you to manage drafts for your content.

**中文译文:** Draft & Publish 功能用于管理内容的 draft 版本。

**Original:** Plan: Free feature. Role & permission: None. Activation: available but disabled by default. Environment: Development & Production.

**中文译文:** 功能属性：Free feature；无额外 role/permission 要求；功能可用但默认关闭；Development 与 Production environment 均支持。

## Configuration

**Original:** Path: Content Type Builder. Enable Draft & Publish for each content type from Advanced settings.

**中文译文:** 配置路径：*Content-Type Builder*。Draft & Publish 按 content type 单独配置。

**Original:** 1. Edit or create a content type.
2. Open Advanced settings.
3. Tick Draft & Publish.
4. Click **Finish**.

**中文译文:** 1. 编辑已有 content type，或创建新 content type；
2. 打开 **Advanced settings**；
3. 勾选 Draft & Publish；
4. 点击 **Finish**。

**Original:** When Draft & Publish is enabled, `status` is a reserved attribute name. You cannot add a user-defined `status` attribute or enable Draft & Publish on a content type that already has one. Strapi 5 warns if a migrated Strapi v4 content type inherited this attribute.

**中文译文:** 启用 Draft & Publish 后，`status` 会成为 Strapi 保留 attribute name。不能为该 content type 添加用户自定义 `status` attribute，也不能在已经拥有 `status` attribute 的 content type 上启用 Draft & Publish。从 Strapi v4 迁移而来的 content type 如果继承了该 attribute，Strapi 5 会在 bootstrap 时记录 warning。重新启用 Draft & Publish 前应先重命名，详见 migration guide。

### Recording the first publication date

**Original:** When the `experimental_firstPublishedAt` future flag is enabled, Strapi adds a `firstPublishedAt` attribute to all Draft & Publish content types. It stores the first publication date and never changes on later unpublish/re-publish.

**中文译文:** 启用 `experimental_firstPublishedAt` future flag 后，Strapi 会为所有使用 Draft & Publish 的 content-types 自动添加 `firstPublishedAt` attribute。它记录 entry 第一次 publish 的日期与时间；之后即使 unpublish 再 publish，也不会改变。

**Original:** Disabling the feature flag later removes the `firstPublishedAt` attribute and its stored values.

**中文译文:** 如果之后关闭该 feature flag，`firstPublishedAt` attribute 及其已存储值会被移除。

## Usage

**Original:** With Draft & Publish enabled, an entry has three statuses:
- Published: previously published, no pending saved draft changes.
- Modified: previously published, draft changes have been saved but not published.
- Draft: never published.

**中文译文:** 启用 Draft & Publish 后，entry 可能有 3 种状态：
- **Published**：之前已经 publish，当前没有等待发布的已保存 draft change；
- **Modified**：之前已经 publish，但 draft 中又保存了尚未 publish 的修改；
- **Draft**：内容从未 publish。

**Original:** In Content Manager list view, entries can be filtered and sorted by publication status.

**中文译文:** 在 Content Manager list view 中，可以使用 **Filters** 按 status 筛选 entries，也可以点击 **Status** column header 按 publication status 排序。

### Working with drafts

**Original:** The edit view shows Draft and Published tabs. Draft is editable; Published is read-only and shows the current live version.

**中文译文:** Edit view 包含 *Draft* 和 *Published* 两个 tabs。*Draft* 用于编辑；*Published* 为 read-only，只显示当前线上 published version。若 document 从未 publish，则无法打开 *Published* tab。

**Original:** New content starts as a draft. You can Save, Publish, or Discard changes.

**中文译文:** 新建内容默认是 draft。可以随时使用 **Save** 保存，点击 **Publish** 发布，或者在 Entry 区域菜单中选择 **Discard changes** 放弃修改。

### Publishing a draft

**Original:** Click **Publish** in the Entry box. After publishing, Draft and Published content match and status becomes Published.

**中文译文:** 在右侧 *Entry* 区域点击 **Publish**。发布后，*Draft* 与 *Published* 内容应完全一致（Published 仍为 read-only），status 变为 **Published**。

**Original:** Before publishing, ensure the draft does not relate to unpublished content, otherwise some content may be unavailable through the API.

**中文译文:** Publish 前应确认 draft 不依赖其他尚未 publish 的内容，否则通过 API 获取时部分关联内容可能不可用。

**Original:** To schedule publication, add the draft to a release and schedule that release.

**中文译文:** 如果需要定时 publish，可以将 draft 加入 release 并安排 release 的发布时间，详见 [Releases](/cms/features/releases)。

### Unpublishing content

**Original:** From the Draft tab, open the Entry menu and choose **Unpublish**.

**中文译文:** 在 *Draft* tab 中，打开右侧 *Entry* 菜单，选择 **Unpublish**。

**Original:** If draft and published content differ, choose:
- Unpublish and keep last draft: preserve the current Draft content and remove Published content.
- Unpublish and replace last draft: discard current Draft content and replace it with Published content.
Then confirm.

**中文译文:** 如果 draft version 与 published version 内容不同，unpublish 时可以选择：
- **Unpublish and keep last draft**：保留当前 *Draft* 内容，并移除 *Published* 内容；
- **Unpublish and replace last draft**：丢弃当前 *Draft* 内容，并用 *Published* 中的内容覆盖 draft。
最后点击 **Confirm**。

### Bulk actions

**Original:** In Content Manager list view, selecting multiple entries enables bulk publish and unpublish. If i18n is enabled, bulk actions only affect the selected locale.

**中文译文:** 在 Content Manager list view 中选择多个 entries 后，可以进行 bulk publish / unpublish。如果启用了 Internationalization，bulk actions 只作用于当前选中的 locale。

#### Bulk publishing drafts

**Original:** 1. Select entries.
2. Click **Publish** above the table.
3. Review each selected entry: Ready to publish or validation errors.
4. Fix errors if needed and click **Refresh**.
5. Click **Publish**.
6. Confirm **Publish**.

**中文译文:** 1. 在 list view 中勾选要发布的 entries；
2. 点击 table header 上方的 **Publish**；
3. 在 *Publish entries* dialog 中检查状态：**Ready to publish** 表示可以发布；required / too short / too long 等红色提示表示无法发布；
4. 如有问题，点击 edit 修复，并使用 **Refresh** 更新 dialog，直到所有 entries 均 Ready to publish；
5. 点击 **Publish**；
6. 在 confirmation dialog 再次点击 **Publish**。

#### Bulk unpublishing content

**Original:** 1. Select entries.
2. Click **Unpublish**.
3. Confirm **Unpublish**.

**中文译文:** 1. 在 Content Manager list view 勾选需要 unpublish 的 entries；
2. 点击 **Unpublish**；
3. 在 confirmation dialog 再次点击 **Unpublish**。

### Usage with APIs

**Original:** Draft or published content can be managed using the `status` parameter through Content API. Publication-related groups such as never-published or modified documents can be queried with `publicationFilter` in REST/GraphQL or the equivalent Document Service option.

**中文译文:** Draft 或 published content 可以通过 Content API 的 `status` parameter 进行查询、创建、更新和删除。如果需要按 draft/published 关系查询，例如 never-published 或 modified documents，可使用 REST / GraphQL 的 `publicationFilter`，或 Document Service API 的等价 option。

**Original:** REST, GraphQL, and Document Service API all support publication status operations.

**中文译文:** 相关文档：[REST status](/cms/api/rest/status)、[REST publicationFilter](/cms/api/rest/publication-filter)、[GraphQL status/publicationFilter](/cms/api/graphql#status)、[Document Service status](/cms/api/document-service/status)、[Document Service publicationFilter](/cms/api/document-service/publication-filter)。
