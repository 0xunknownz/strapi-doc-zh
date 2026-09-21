# 📖 对照翻译：Releases

> Source: `docusaurus/docs/cms/features/releases.md`  
> Upstream SHA: `8502a6bf34fb0c21c1c7c2257284d10214727b43`

**Original:** Releases group entries into publishable batches to trigger simultaneous publish or unpublish actions across content types and locales.

**中文译文:** Releases 可以把多个 entries 组织为可统一执行的发布批次，让不同 content types、不同 locales 的内容同时 publish 或 unpublish。

**Original:** The Releases feature enables content managers to organize entries into containers that can perform publish and unpublish actions simultaneously. A release can contain entries from different content types and can mix locales.

**中文译文:** Releases 功能允许 content manager 把 entries 放入同一个 release container，并在执行 release 时同时完成 publish / unpublish。一个 release 可以包含不同 content types 的 entries，也可以混合多个 locales。

**Original:** Plan: CMS Growth and Enterprise plans. Role & permission: Administrator role. Activation: available by default if plan allows it. Environment: Development & Production.

**中文译文:** 功能属性：需要 CMS Growth 或 Enterprise plan；面向项目 admin panel 中的 Administrator role；满足方案条件时默认可用；Development 与 Production environment 均支持。

## Configuration

**Original:** Before content can be included, scheduled, and published in releases, releases must be created. You can also configure the default timezone and delete obsolete releases.

**中文译文:** 在把内容加入 release、安排 schedule 或执行发布前，需要先创建 release。还可以修改 release scheduling 使用的 default timezone，并删除不再需要的 releases。

### Choosing default timezone

**Original:** Path: Settings. Select Default timezone, choose a timezone, and click **Save**.

**中文译文:** 配置路径：*Settings*。打开 *Default timezone* 下拉列表，选择默认 timezone，然后点击 **Save**。

### Creating a release

**Original:** Path: Releases.
1. Click **New Release**.
2. Give the release a name.
3. Optionally check **Schedule release** and define date, time, and timezone.
4. Click **Continue**.

**中文译文:** 配置路径：*Releases*。
1. 点击右上角 **New Release**；
2. 输入 release name；
3. （可选）如果希望自动定时发布，勾选 **Schedule release**，并设置 date、time 和 timezone；
4. 点击 **Continue**。

**Original:** Releases can be renamed later using the menu and Edit.

**中文译文:** Release 创建后仍可以通过菜单中的 **Edit** 重命名。

### Deleting a release

**Original:** Deleting a release deletes only the release itself, not the content-type entries inside it.
1. Open the top-right menu.
2. Select **Delete**.
3. Confirm.

**中文译文:** 删除 release 只会删除 release container 本身，不会删除其中包含的 content-type entries。
1. 打开 admin panel 右上角菜单；
2. 选择 **Delete**；
3. 在 confirmation dialog 中点击 **Confirm**。

## Usage

**Original:** Releases require Draft & Publish to be enabled for the content type.

**中文译文:** Releases 的发布操作本质上是把 draft entry 转为 published entry，因此如果 content-type 没有启用 [Draft & Publish](/cms/features/draft-and-publish)，Releases 无法正常使用。

### Including content in a release

**Original:** Before adding entries, create a release and ensure you have the appropriate Content-Releases plugin permissions.

**中文译文:** 添加 entries 前，需要先在 *Releases* 页面创建 release，并确保当前 administrator role 拥有 Content-Releases plugin 对应权限。

**Original:** A release stores a reference to an entry, not a copy. If the draft changes after it is added, the release publishes the latest saved draft. A release cannot be pinned to an earlier version.

**中文译文:** Release 保存的是 entry reference，而不是 entry 内容副本。如果 draft 在加入 release 后继续修改，release 最终会发布**最新保存的 draft**，而不是加入 release 当时的内容。Release 不能锁定到特定 version；若需要发布历史版本，应先通过 [Content History](/cms/features/content-history) restore 为当前 draft。

#### One entry at a time

**Original:** 1. In Content Manager edit view, open the Entry menu.
2. Click **Add to release**.
3. Select a release.
4. Choose **Publish** or **Unpublish** and click **Continue**.

**中文译文:** 1. 在 Content Manager edit view 中打开右侧 *Entry* 菜单；
2. 点击 **Add to release**；
3. 选择目标 release；
4. 根据 release 执行时希望对该 entry 做的操作选择 **Publish** 或 **Unpublish**，然后点击 **Continue**。

**Original:** The Releases box shows which releases include the entry. Scheduled releases also show their date and time.

**中文译文:** 右侧 *Releases* 区域会显示当前 entry 已加入哪些 releases。如果 release 已 schedule，还会显示计划执行的 date / time。

#### Multiple entries at a time

**Original:** 1. Select entries in Content Manager list view.
2. Click **Add to release**.
3. Select the release.
4. Choose **Publish** or **Unpublish**, then **Continue**.

**中文译文:** 1. 在 Content Manager list view 中勾选多个 entries；
2. 点击 table 上方的 **Add to release**；
3. 选择目标 release；
4. 选择 **Publish** 或 **Unpublish**，然后点击 **Continue**。

### Removing content from a release

**Original:** In the Releases box, open the menu below the release name and click **Remove from release**.

**中文译文:** 在 edit view 右侧 *Releases* 区域中，打开 release name 下方菜单，点击 **Remove from release**。

### Scheduling a release

**Original:** Releases can be published manually or scheduled for a date/time/timezone. Scheduling can be configured at creation or later through Edit.

**中文译文:** Release 可以手动 publish，也可以按指定 date、time 和 timezone 自动 publish。Schedule 可以在创建 release 时配置，也可以之后通过 **Edit** 添加或修改。

**Original:** To schedule an existing release:
1. Open the top-right menu.
2. Select **Edit**.
3. Check **Schedule release**.
4. Select date, time, timezone.
5. Click **Save**.

**中文译文:** 为现有 release 设置 schedule：
1. 打开右上角菜单；
2. 选择 **Edit**；
3. 勾选 **Schedule release**；
4. 设置 date、time、timezone；
5. 点击 **Save**。

### Publishing a release

**Original:** Publishing a release performs all configured publish and unpublish actions simultaneously.

**中文译文:** Publish release 时，会同时执行 release 中所有 entries 已配置的 publish / unpublish actions。

**Original:** Release statuses:
- Empty: no entries.
- Blocked: at least one entry prevents publishing.
- Ready: content exists and all checks pass.
- Done: release was executed.

**中文译文:** Release status：
- **Empty**：尚未添加 entry；
- **Blocked**：已添加内容，但至少一个 entry 存在问题，阻止 release 执行；
- **Ready**：已添加内容，并且所有 checks 通过，可以 publish；
- **Done**：release 已经执行完成。

**Original:** Entry statuses include Already published, Already unpublished, Ready to publish, Ready to unpublish, and Not ready to publish.

**中文译文:** Entry status 可能包括 **Already published**、**Already unpublished**、**Ready to publish**、**Ready to unpublish** 和 **Not ready to publish**。如果存在 Not ready entry，release 会保持 Blocked，直到问题修复。

**Original:** If a release is blocked, edit problematic entries, fix issues, and click **Refresh** to update status.

**中文译文:** 如果 release 为 Blocked，可通过 entry 菜单进入 **Edit the entry** 修复问题；修复后点击 **Refresh** 更新 release page 状态。

**Original:** Once a release is published, it cannot be updated or re-released. Create another release for later changes.

**中文译文:** Release 一旦 publish，就不能继续更新，也不能用同一个 release 重新执行修改后的同一批 entries；后续需要创建新的 release。

### Audit logging of release actions

**Original:** Enterprise plan users have release actions automatically recorded in Audit Logs, including changes made by the admin panel or scheduled jobs.

**中文译文:** Enterprise plan 中，Release actions 会自动记录到 [Audit Logs](/cms/features/audit-logs)，无论 action 来自 admin panel 还是 scheduled job。

**Original:** Recorded actions include create/update/delete/trigger release, add/change/remove entry, and update release settings.

**中文译文:** 会记录的 actions 包括：create release、update release、delete release、trigger release、add entry、change entry action、remove entry，以及 update release settings。

**Original:** Log records include actor, origin (`admin` or `scheduler`), and affected resource. Deleting an entry or locale that belongs to a pending release does not count as an explicit "Remove entry from release" event.

**中文译文:** 每条 log 都包含 actor、origin（`admin` 或 `scheduler`）以及受影响的 resource。如果某个 pending release 中的 entry 或 locale 本身被删除，这不会生成显式的 “Remove entry from release” log；entry / locale 的 delete action 会单独记录。
