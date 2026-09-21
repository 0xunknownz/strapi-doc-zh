# 📖 对照翻译：Review Workflows

> Source: `docusaurus/docs/cms/features/review-workflows.md`  
> Upstream SHA: `efed88ec426301a8f8ff2562c9c73e3ec594d280`

**Original:** Review Workflows define custom multi-stage pipelines for content review, facilitating collaboration from draft to publication.

**中文译文:** Review Workflows 用于定义自定义、多阶段的内容审核 pipeline，帮助团队从 draft 到 publication 的整个流程中协作。

**Original:** The Review Workflows feature allows you to create and manage workflows for your various content-types. Each workflow can consist of any review stages, enabling collaboration in the content creation flow from draft to publication.

**中文译文:** Review Workflows 可以为不同 content-types 创建和管理 workflow。每个 workflow 可以包含任意数量的 review stages，让团队在内容从 draft 到 publication 的过程中协同工作。

**Original:** Plan: CMS Enterprise Plan. Role & permission: Super Admin. Activation: available by default if required plan. Environment: Development & Production.

**中文译文:** 功能属性：需要 CMS Enterprise Plan；默认面向 Super Admin；满足方案条件时可用；Development 与 Production environment 均支持。

## Configuration

**Original:** Path: Settings > Global settings > Review Workflows.

**中文译文:** 配置路径：*Settings > Global settings > Review Workflows*。

**Original:** To use review workflows in Content Manager, configure the default workflow or create a new one. The default workflow has 4 stages: To do, In progress, Ready to review, and Reviewed. All can be edited, reordered, deleted, and new stages can be added.

**中文译文:** 要在 Content Manager 中使用 Review Workflows，需要配置默认 workflow，或者创建新 workflow。默认 workflow 包含 4 个 stages：To do、In progress、Ready to review、Reviewed。它们都可以编辑、重新排序、删除，也可以添加新 stage。

### Creating a new workflow

**Original:** 1. Click **Create new workflow** or edit an existing workflow.
2. Configure:

| Setting name | Instructions |
| --- | --- |
| Workflow name | Write a unique name. |
| Associated to | (optional) Assign the workflow to content-types. |
| Stages | Add review stages. |

3. Click **Save**.

**中文译文:** 1. 点击 **Create new workflow**，或 edit 某个现有 workflow；
2. 配置：

| 设置项 | 说明 |
| --- | --- |
| Workflow name | 输入唯一 workflow name。 |
| Associated to | （可选）把 workflow 分配给一个或多个现有 content-types。 |
| Stages | 添加 review stages。 |

3. 点击 **Save**。新 workflow 会出现在列表中，并应用到已关联的 content-types。

**Original:** The maximum number of workflows and stages per workflow is limited.

**中文译文:** 每个方案允许的 workflow 数量以及单个 workflow 中的 stage 数量都有上限，具体以 Strapi 当前 pricing 规则为准。

### Editing a workflow

#### Adding a new stage

**Original:** 1. Click **Add new stage**.
2. Write the Stage name.
3. Select a Color.
4. Select Roles that can change from this stage.
5. Select Roles that can move content to this stage.
6. Click **Save**.

**中文译文:** 1. 点击 **Add new stage**；
2. 输入 *Stage name*；
3. 选择 *Color*；
4. 选择 *Roles that can change from this stage*，定义哪些 roles 可以把内容移出该 stage；
5. 选择 *Roles that can move content to this stage*，定义哪些 roles 可以把内容移入该 stage；
6. 点击 **Save**。

**Original:** New stages are appended by default but can be reordered. Each permission field has an "Apply to all stages" option. You can also use "Duplicate stage" to copy the whole stage configuration.

**中文译文:** 新 stage 默认追加到末尾，但可以随时重新排序。每个 permission field 都有 **Apply to all stages**，可把对应 role selection 复制到其他 stages；也可以使用 **Duplicate stage** 复制整套 stage configuration。

#### Duplicating a stage

**Original:** 1. Click **Duplicate Stage** in the stage context menu.
2. Change the duplicated stage name.
3. Click **Save**.

**中文译文:** 1. 在 stage context menu 中点击 **Duplicate Stage**；
2. 修改复制后的 stage name；
3. 点击 **Save**。

#### Deleting a stage

**Original:** Delete a stage from its context menu. If it has pending reviews, they move to the first stage. Every workflow must contain at least one stage, so the final stage cannot be deleted.

**中文译文:** 可以从 stage context menu 中删除 stage。如果该 stage 中存在 pending reviews，它们会被移动到 workflow 的第一个 stage。每个 workflow 至少必须保留一个 stage，因此最后一个 stage 不能删除。

### Deleting a workflow

**Original:** Delete a workflow from the list view. It is not possible to delete the last workflow.

**中文译文:** 可以在 list view 中删除 workflow，但不能删除最后一个 workflow。

## Usage

**Original:** Path: Content Manager.

**中文译文:** 使用路径：*Content Manager*。

### Changing review stage

**Original:** Available target stages depend on the current user's role permissions: the user must be allowed to move content from the current stage and into the target stage.

**中文译文:** 可选择的 target stages 取决于当前用户的 role permissions：用户既要有权限把内容移出 current stage，也要有权限把内容移入 target stage。

**Original:** 1. Open the content-type edit view.
2. In the Review Workflows box, open the Review stage dropdown.
3. Choose the new review stage. It is saved automatically.

**中文译文:** 1. 打开 content-type edit view；
2. 在右侧 *Review Workflows* 区域打开 *Review stage* 下拉列表；
3. 选择新的 review stage。变更会自动保存。

### Defining assignee

**Original:** Entries in a review workflow content type can be assigned to any admin user for review.

**中文译文:** Review workflow content type 中的 entry 可以分配给任意 Strapi admin user 进行 review。

**Original:** 1. Open the content-type edit view.
2. In Review Workflows, open the Assignee dropdown.
3. Choose the new assignee. It is saved automatically.

**中文译文:** 1. 打开 content-type edit view；
2. 在 *Review Workflows* 区域打开 *Assignee* 下拉列表；
3. 选择新的 assignee。变更会自动保存。

**Original:** You can filter entries in Content Manager by Assignee and Review Stage.

**中文译文:** 可以在 Content Manager list view 中按 **Assignee** 和 **Review Stage** 筛选 entries。
