# 📖 对照翻译：Cloud project settings

> Source: `docusaurus/docs/cloud/projects/settings.md`  
> Upstream SHA: `e8df5f66b6ba4668564712c8143a298893569853`

**Original:** Cloud project settings

**中文译文:** Cloud 项目设置

**Original:** Settings area spans project-level controls (general, billing & invoices, plans) and per-environment configuration.

**中文译文:** Settings 区域同时涵盖项目级控制项（General、Billing & Invoices、Plans）以及每个 environment 的独立配置。

**Original:** From a chosen project's dashboard, the **Settings** button, located in the header, enables you to manage the configurations and settings for your Strapi Cloud project and its environments.

**中文译文:** 在选定项目的 dashboard 中，可以通过 header 里的 **Settings** 按钮管理 Strapi Cloud 项目及其各个 environments 的配置与设置。

**Original:** The settings' menu on the left side of the interface is separated into 2 categories: the settings for the entire project and the settings specific to any configured environment for the project.

**中文译文:** 界面左侧的 settings 菜单分为两类：整个项目的项目级设置，以及针对项目中各个已配置 environment 的独立设置。

## Project-level settings

**Original:** There are 4 tabs available for the project settings:
- *General*,
- *Environments*,
- *Billing & Invoices*,
- and *Plans*.

**中文译文:** 项目级设置包含 4 个标签页：
- *General*；
- *Environments*；
- *Billing & Invoices*；
- *Plans*。

### General

**Original:** The *General* tab for the project-level settings enables you to check and update the following options for the project:

- *Basic information*, to see:
  - the name of your Strapi Cloud project — used to identify the project on the Cloud Dashboard, Strapi CLI, and deployment URLs — and change it.
  - the chosen hosting region for your Strapi Cloud project, meaning the geographical location of the servers where the project and its data and resources are stored. The hosting region is set at project creation and cannot be modified afterwards.
  - the project's metadata, including the Production app internal name and the Subscription ID, which can be useful for debugging & support purposes.
- *Strapi CMS license key*: to enable and use some CMS features directly on your Cloud project.
- *Connected Git repository*: to change the repository and branch used for your project. Also allows you to enable/disable the "deploy on push" option.
- *Danger zone*, with:
  - *Transfer ownership*: for the project owner to transfer the ownership of the Cloud project to an already existing maintainer.
  - *Delete project*: to permanently delete your Strapi Cloud project.

**中文译文:** 项目级设置中的 *General* 标签页可以查看并更新以下项目选项：

- *Basic information*，用于查看：
  - Strapi Cloud 项目名称。该名称用于在 Cloud Dashboard、Strapi CLI 和 deployment URLs 中识别项目，也可以在这里修改；
  - Strapi Cloud 项目所选的 hosting region，即存储项目及其数据与资源的服务器所在地区。hosting region 在创建项目时确定，之后无法修改；
  - 项目 metadata，包括 Production app internal name 和 Subscription ID，这些信息在调试和请求支持时可能有用。
- *Strapi CMS license key*：为 Cloud 项目启用并使用额外的 CMS 功能；
- *Connected Git repository*：修改项目所使用的 repository 和 branch，也可以启用或禁用 “deploy on push”；
- *Danger zone*：
  - *Transfer ownership*：由项目 owner 将 Cloud 项目的所有权转移给现有 maintainer；
  - *Delete project*：永久删除 Strapi Cloud 项目。

#### Renaming project

**Original:** The project name is set at project creation and can be modified afterwards via the project settings.

**中文译文:** 项目名称在创建项目时设置，之后可以通过项目 settings 修改。

**Original:**
1. In the *Basic information* section of the *General* tab, click on the edit button.
2. In the dialog, write the new project name of your choice in the *Project name* textbox.
3. Click on the **Rename** button to confirm the project name modification.

**中文译文:**
1. 在 *General* 标签页的 *Basic information* 区域，点击编辑按钮；
2. 在对话框的 *Project name* 文本框中输入新的项目名称；
3. 点击 **Rename** 确认修改。

#### Adding a CMS license key

**Original:** A CMS license key can be added and connected to a Strapi Cloud project to unlock additional Strapi CMS features across all of the project’s environments. The CMS features that will be accessible via the license key depend on the type of license that was purchased. Please refer to the Strapi Pricing page for more information and/or to purchase a license.

**中文译文:** 可以向 Strapi Cloud 项目添加并关联 CMS license key，从而在项目的所有 environments 中解锁额外的 Strapi CMS 功能。license key 能够启用哪些 CMS 功能取决于购买的 license 类型。更多信息或购买 license，请参阅 Strapi Pricing 页面。

**Original:** If you don't see the *Strapi CMS license key* section, it probably means that your subscription is a legacy one and does not support custom CMS licenses. It means that you already have one that is automatically included on your project.

**中文译文:** 如果没有看到 *Strapi CMS license key* 区域，通常表示你的 subscription 属于 legacy 方案，不支持自定义 CMS license；这种情况下，项目一般已经自动包含了对应 license。

**Original:**
1. In the *Strapi CMS license key* section, click on the **Add license** button.
2. In the dialog, paste your license key in the field.
3. Click on the **Save & deploy** button for the changes to take effect.

**中文译文:**
1. 在 *Strapi CMS license key* 区域点击 **Add license**；
2. 在对话框中粘贴 license key；
3. 点击 **Save & deploy**，使变更生效。

**Original:** To remove the Strapi CMS license from your Strapi Cloud project, you can click on the **Unlink license** button. This will also remove access and usage to the CMS features included in the previously added license.

**中文译文:** 若要从 Strapi Cloud 项目移除 Strapi CMS license，可以点击 **Unlink license**。移除后，项目也将失去此前 license 所包含 CMS 功能的访问和使用权限。

**Original:** The license key is applied to all the environments in the project.

**中文译文:** license key 会应用到该项目的所有 environments。

#### Modifying git repository & branch

**Original:** The GitHub or GitLab repository, branch and base directory for a Strapi Cloud project are by default chosen at the creation of the project. After the project's creation, via the project settings, it is possible to update the project repository or switch to another git provider.

**中文译文:** Strapi Cloud 项目的 GitHub 或 GitLab repository、branch 和 base directory 默认在创建项目时选择。项目创建完成后，可以通过项目 settings 更新 repository，或者切换到其他 Git provider。

**Original:** Updating the git repository could result in the loss of the project and its data, for instance if the wrong repository is selected or if the data schema between the old and new repository doesn't match.

**中文译文:** 更新 Git repository 可能导致项目及其数据丢失，例如误选 repository，或者新旧 repository 的数据 schema 不一致时。执行此操作前应确认 repository 与 schema 均正确。

**Original:**
1. In the *Connected git repository* section of the *General* tab, click on the **Update repository** button. You will be redirected to another interface.
2. (optional) If you wish to not only update the repository but switch to another git provider, click on the **Switch Git provider** button at the top right corner of the interface. You will be redirected to the chosen git provider's authorization settings before getting back to the *Update repository* interface.
3. In the *Update repository* section, fill in the 2 available settings:

| Setting name | Instructions |
| --- | --- |
| Account | Choose an account from the drop-down list. |
| Repository | Choose a repository from the drop-down list. |

4. In the *Select Git branches* section, fill in the available settings for any of your environments. Note that the branch can be edited per environment via its own settings.

| Setting name | Instructions |
| --- | --- |
| Branch | Choose a branch from the drop-down list. |
| Base directory | Write the path of the base directory in the textbox. |
| Auto-deploy | Tick the box to automatically trigger a new deployment whenever a new commit is pushed to the selected branch. Untick it to disable the option. |

5. Click on the **Save & deploy** button for the changes to take effect.

**中文译文:**
1. 在 *General* 标签页的 *Connected git repository* 区域点击 **Update repository**，系统会跳转到新的界面；
2. （可选）如果除了更新 repository 之外还要切换 Git provider，点击界面右上角的 **Switch Git provider**。完成所选 provider 的授权设置后，会返回 *Update repository* 界面；
3. 在 *Update repository* 区域配置以下项目：

| 设置名称 | 说明 |
| --- | --- |
| Account | 从下拉列表选择 account。 |
| Repository | 从下拉列表选择 repository。 |

4. 在 *Select Git branches* 区域，为各个 environments 配置：

| 设置名称 | 说明 |
| --- | --- |
| Branch | 从下拉列表选择 branch。 |
| Base directory | 在文本框中填写 base directory 路径。 |
| Auto-deploy | 勾选后，每当新 commit 推送到所选 branch 时自动触发 deployment；取消勾选即可关闭。 |

5. 点击 **Save & deploy** 使变更生效。

#### Transferring project ownership

**Original:** The ownership of the Strapi Cloud project can be transferred to another user, as long as they're a maintainer of the project. It can either be at the initiative of the current project owner, or can be requested by a project maintainer. Once the ownership is transferred, it is permanent until the new owner decides to transfer the ownership again to another maintainer.

**中文译文:** 只要目标用户已经是项目 maintainer，就可以把 Strapi Cloud 项目的所有权转移给该用户。转移既可以由当前 project owner 主动发起，也可以由 maintainer 提出请求。所有权转移完成后会持续有效，除非新的 owner 再次将所有权转移给其他 maintainer。

**Original:** For the ownership of a project to be transferred, the following requirements must be met:
- The project must not currently have expired card and/or unpaid bills.
- The maintainer must have filled their billing information.
- No already existing ownership transfer must be pending for the project.

Note that ownership transfers might fail when done the same day of subscription renewal (i.e. 1st of every month). If the transfer fails that day, but all prerequisites are met, you should wait a few hours and try again.

**中文译文:** 转移项目所有权前必须满足以下条件：
- 项目当前不能存在过期银行卡和/或未支付账单；
- maintainer 必须已经填写 billing information；
- 项目不能已经存在尚未完成的 ownership transfer。

如果在 subscription 续订当天（即每月 1 日）执行，ownership transfer 可能失败。若所有前置条件都满足但当天仍失败，可等待数小时后重试。

**Original:**
1. In the *Danger zone* section of the *General* tab, click on the **Transfer ownership** button.
2. In the dialog:
   - If you are the project owner: choose the maintainer who should be transferred the ownership by clicking on **...** > **Transfer ownership** associated with their name.
   - If you are a maintainer: find yourself in the list and click on **...** > **Transfer ownership** associated with your name.
3. Confirm the transfer/request in the new dialog by clicking on the **Transfer ownership** button.

**中文译文:**
1. 在 *General* 标签页的 *Danger zone* 中点击 **Transfer ownership**；
2. 在对话框中：
   - 如果你是 project owner：找到要接收所有权的 maintainer，点击其名称对应的 **...** > **Transfer ownership**；
   - 如果你是 maintainer：在列表中找到自己，点击对应的 **...** > **Transfer ownership**；
3. 在新的对话框中点击 **Transfer ownership**，确认转移或请求。

**Original:** An email will be sent to both users. The person who needs to transfer the ownership or inherit it will have to click on the **Confirm transfer** button in the email. Once done, the previous owner will receive a confirmation email that the transfer has successfully been done.

**中文译文:** 系统会向双方发送邮件。需要转出或接收所有权的一方必须点击邮件中的 **Confirm transfer**。完成后，原 owner 会收到一封确认 ownership transfer 已成功完成的邮件。

**Original:** As long as the ownership transfer or request hasn't been confirmed, there is the option to cancel in the same dialog that the maintainer was chosen.

**中文译文:** 在 ownership transfer 或请求尚未确认之前，可以在选择 maintainer 的同一个对话框中取消操作。

**Original:** Once the ownership transfer is done, the project will be disconnected from Strapi Cloud. As new owner, make sure to go to the *General* tab of project settings to reconnect the project.

**中文译文:** ownership transfer 完成后，项目会与 Strapi Cloud 断开连接。新的 owner 需要进入项目 settings 的 *General* 标签页重新连接项目。

#### Deleting a Strapi Cloud project

**Original:** You can delete any Strapi Cloud project, but it will be permanent and irreversible. Associated domains, deployments and data will be deleted and the subscription for the project will automatically be canceled.

**中文译文:** 可以删除任意 Strapi Cloud 项目，但该操作永久且不可逆。相关 domains、deployments 和数据都会被删除，同时项目 subscription 会自动取消。

**Original:**
1. In the *Danger zone* section of the *General* tab, click on the **Delete project** button.
2. In the dialog, select the reason for deleting your project.
3. Confirm the deletion of your project by clicking on the **Delete project** button.

**中文译文:**
1. 在 *General* 标签页的 *Danger zone* 中点击 **Delete project**；
2. 在对话框中选择删除项目的原因；
3. 点击 **Delete project** 确认删除。

### Environments

**Original:** The *Environments* tab allows you to see all configured environments for the Strapi Cloud project, as well as to create new ones. Production is the default environment, which cannot be deleted. Other environments can be created (depending on the subscription plan for your project) to work more safely on isolated instances of your Strapi Cloud project (e.g. a staging environment where tests can be made before being available on production).

**中文译文:** *Environments* 标签页可以查看 Strapi Cloud 项目中所有已配置 environments，也可以创建新的 environment。Production 是默认 environment，不能删除。根据项目的 subscription plan，可以创建其他相互隔离的 environments，以更安全地开展工作，例如先在 staging environment 中测试，再发布到 production。

**Original:** The billing cycle of additional environments you purchase will match the billing cycle of your plan.

**中文译文:** 额外购买的 environments 会沿用当前方案的 billing cycle。

**Original:** To create a new environment:

1. Click on the **Add a new environment** button.
2. In the setup step, fill in the available settings:

| Setting name | Instructions |
| --- | --- |
| Environment name | (mandatory) Write a name for your project's new environment. |
| Git branch | (mandatory) Select the right branch for your new environment. |
| Base directory | Write the name of the base directory of your new environment. |
| Deploy on push | Tick this box to automatically trigger a deployment when changes are pushed to your selected branch. When disabled, you will need to manually deploy the latest changes. |
| Import variables | Tick the box to import variable names from an existing environment. Values will not be imported, and all variables will remain blank. |

3. Click **Confirm** to proceed to the checkout step.
4. Review the environment price, applicable taxes and proration adjustment.
5. Click on the **Add environment** button to create your project's new environment. You will then be redirected to your *Project dashboard* where you will be able to follow your new environment's creation and first deployment.

**中文译文:** 创建新 environment：

1. 点击 **Add a new environment**；
2. 在 setup 步骤配置以下设置：

| 设置名称 | 说明 |
| --- | --- |
| Environment name | （必填）填写新 environment 的名称。 |
| Git branch | （必填）选择新 environment 对应的 branch。 |
| Base directory | 填写新 environment 的 base directory 名称。 |
| Deploy on push | 勾选后，所选 branch 有变更推送时自动触发 deployment；关闭后需要手动部署最新变更。 |
| Import variables | 勾选后从已有 environment 导入变量名称。**变量值不会导入，所有变量值均保持为空。** |

3. 点击 **Confirm** 进入 checkout；
4. 检查 environment 价格、适用税费以及 proration adjustment；
5. 点击 **Add environment** 创建 environment。随后会跳转到 *Project dashboard*，可以跟踪 environment 的创建过程和首次 deployment。

**Original:** If an error occurs during the environment creation, the progress indicator will stop and display an error message. You will see a **Retry** button next to the failed step, allowing you to restart the creation process.

**中文译文:** 如果创建 environment 期间发生错误，进度指示器会停止并显示错误消息。失败步骤旁会出现 **Retry** 按钮，可从该步骤重新启动创建流程。

### Billing & Invoices

**Original:** The *Billing & Invoices* tab displays your subscription details and the full list of invoices for your Strapi Cloud project.

**中文译文:** *Billing & Invoices* 标签页展示 Strapi Cloud 项目的 subscription 详情以及完整 invoice 列表。

**Original:** Only project owners can access the *Billing & Invoices* tab. Maintainers do not have access to this tab.

**中文译文:** 只有 project owner 可以访问 *Billing & Invoices* 标签页；maintainers 无法访问。

**Original:** Through this tab, you can:
- click the **Change** button to be redirected to the *Plans* tab, where you can change your subscription plan or billing cycle,
- click the **Edit** button to set a new payment method.

**中文译文:** 在该标签页中可以：
- 点击 **Change** 跳转到 *Plans* 标签页，修改 subscription plan 或 billing cycle；
- 点击 **Edit** 设置新的 payment method。

**Original:** You can attach a dedicated card to your project by choosing the payment method directly from this page, allowing you to manage your subscriptions with different cards.

**中文译文:** 可以直接在此页面选择 payment method，为项目绑定专用银行卡，从而使用不同银行卡分别管理不同 subscriptions。

**Original:** The tab also lists all invoices for your Strapi Cloud project and their status.

**中文译文:** 该标签页还会列出 Strapi Cloud 项目的全部 invoices 及其状态。详细状态说明参见项目内的 `docs/snippets/invoices-statuses.md`。

**Original:** In the *Profile > Invoices* tab, you will find the complete list of invoices for all your projects.

**中文译文:** 在 *Profile > Invoices* 标签页中，可以查看账户下所有项目的完整 invoice 列表。

### Plans

**Original:** The *Plans* tab displays an overview of the available Strapi Cloud plans and allows you to change your current plan, or your billing cycle.

**中文译文:** *Plans* 标签页展示可用 Strapi Cloud plans 的概览，并允许修改当前 plan 或 billing cycle。

**Original:** If your current plan is labeled as *legacy*, you will be able to sidegrade to a new plan. Once you sidegrade, you will no longer have access to your previous plan.

**中文译文:** 如果当前 plan 标记为 *legacy*，可以 sidegrade 到新的 plan。一旦完成 sidegrade，就无法再使用之前的 plan。

#### Upgrading to another plan

**Original:** Plan upgrades are immediate and can be managed, for each project, via the project settings.

**中文译文:** Plan upgrade 会立即生效，并可按项目在 project settings 中分别管理。

**Original:** To upgrade your current plan to a higher one:

1. In the *Plans* tab of your project settings, choose between monthly and yearly billing frequency, and click on the **Upgrade** button of the plan you want to upgrade to.
2. In the window that opens, review the payment details and terms of the upgrade.
   a. (optional) Click the **Edit** button to select another payment method.
   b. (optional) Click **I have a discount code**, enter your discount code in the field, and click on the **Apply** button.
3. Click on the **Upgrade to [plan name]** button to confirm the upgrade. The project will automatically be re-deployed.

**中文译文:** 将当前 plan 升级到更高方案：

1. 在项目 settings 的 *Plans* 标签页中选择 monthly 或 yearly billing frequency，然后点击目标 plan 的 **Upgrade**；
2. 在弹出的窗口中检查付款详情和 upgrade 条款；
   a. （可选）点击 **Edit** 选择其他 payment method；
   b. （可选）点击 **I have a discount code**，输入 discount code 后点击 **Apply**；
3. 点击 **Upgrade to [plan name]** 确认升级。项目会自动重新 deployment。

#### Downgrading to another plan

**Original:** Plan downgrades can be managed, for each project, via the project settings. Downgrades are, however, not immediately effective: the current plan will remain active until the end of the current billing period.

**中文译文:** Plan downgrade 同样可以按项目在 project settings 中管理，但不会立即生效：当前 plan 会持续有效到本计费周期结束。

**Original:** Make sure to check the usage of your Strapi Cloud project before downgrading: if your current usage exceeds the limits of the lower plan, you are taking the risk of getting charged for overages. You may also lose access to some features: for example, downgrading to the Starter plan would result in the loss of all your project's backups.

Note also that you cannot downgrade if you have additional paid environments. You will first need to delete all additional environments that were not included in the base price of your plan before you can schedule a downgrade. When downgrading from Business to Pro, the additional included environment will automatically be deleted when the downgrade takes effect.

**中文译文:** Downgrade 前应先检查 Strapi Cloud 项目的当前 usage。如果当前用量超过较低方案的限制，可能产生 overage 费用；同时也可能失去部分功能。例如 downgrade 到 Starter 后，项目的全部 backups 都会失去。

如果存在额外付费 environments，也不能直接 downgrade。必须先删除所有未包含在当前 plan 基础价格中的额外 environments，之后才能安排 downgrade。从 Business downgrade 到 Pro 时，Business 中额外包含的 environment 会在 downgrade 生效时自动删除。

**Original:** To downgrade your current plan to a lower one:

1. In the *Plans* tab of your project settings, choose between monthly and yearly billing frequency and click on the **Downgrade** button of the plan you want to downgrade to.
2. In the window that opens, review the terms of the downgrade.
3. Click on the **Downgrade** button to confirm the downgrade. The project will automatically be re-deployed.

**中文译文:** 将当前 plan downgrade 到较低方案：

1. 在项目 settings 的 *Plans* 标签页选择 monthly 或 yearly billing frequency，并点击目标 plan 的 **Downgrade**；
2. 在弹出的窗口中检查 downgrade 条款；
3. 点击 **Downgrade** 确认。项目会自动重新 deployment。

**Original:** Downgrades are effective at the end of the current billing period. Whilst the change is pending, you can cancel the scheduled downgrade and stay on your current plan.

**中文译文:** Downgrade 会在当前 billing period 结束时生效。在变更尚未生效期间，可以取消已安排的 downgrade 并继续使用当前 plan。

#### Changing billing cycle

**Original:** You can switch your project's billing cycle between monthly and yearly billing at any time. While project plans and addons can either be billed monthly or yearly depending on your billing cycle, overages are always billed monthly.

**中文译文:** 可以随时在 monthly billing 与 yearly billing 之间切换项目的 billing cycle。Project plans 和 addons 会根据所选 billing cycle 按月或按年计费，但 overages 始终按月计费。

**Original:** To change your billing cycle:

1. In the *Plans* tab of your project settings, use the toggle at the top of the plans section to switch between monthly and yearly billing.
2. Click the **Switch to [monthly/yearly] billing** button of your current plan.
3. In the window that opens, review the terms of the billing cycle change.
4. Click **Confirm switch** to confirm the change.

**中文译文:** 修改 billing cycle：

1. 在项目 settings 的 *Plans* 标签页中，使用 plans 区域顶部的 toggle 在 monthly 与 yearly billing 之间切换；
2. 点击当前 plan 的 **Switch to [monthly/yearly] billing**；
3. 在弹出的窗口中检查 billing cycle 变更条款；
4. 点击 **Confirm switch** 确认。

**Original:** When switching from yearly to monthly billing, your plan will remain on its yearly cycle until your next renewal date. Whilst the change is pending, you can cancel the scheduled change and stay on your current billing cycle. When switching from monthly to yearly, however, the change is immediate.

**中文译文:** 从 yearly 切换为 monthly billing 时，plan 会继续按 yearly cycle 运行到下一次 renewal date；在变更等待生效期间，可以取消已安排的切换。相反，从 monthly 切换为 yearly billing 会立即生效。

## Environment-level settings

**Original:** In the project's environments' settings, you first need to select the environment whose settings you would like to configure, using the dropdown. Depending on the chosen environment, there are 3 to 4 tabs available:

- *Configuration*,
- *Backups*, which are only available for the production environment,
- *Domains*,
- and *Variables*.

**中文译文:** 在项目的 environment-level settings 中，需要先通过下拉菜单选择要配置的 environment。根据所选 environment，会提供 3 到 4 个标签页：

- *Configuration*；
- *Backups*，仅 Production environment 可用；
- *Domains*；
- *Variables*。

### Configuration

**Original:** The *Configuration* tab for the environment-level settings enables you to check and update the following options for the project:

- *Basic information*, to see:
  - the name of your Strapi Cloud project's environment. The environment name is set when it is created and cannot be modified afterwards.
  - the Node version of the environment: to change the Node version of the project.
  - the app's internal name for the environment, which can be useful for debug & support purposes.
- *Connected branch*: to change the branch of the GitHub repository used for your environment. Also allows you to enable/disable the "deploy on push" option.
- *Environment data*: to transfer data from another environment within the same project or to remove all data and assets from the current environment while keeping its settings.
- *Danger zone*: to permanently delete an additional environment.

**中文译文:** Environment-level settings 中的 *Configuration* 标签页可以查看并更新以下选项：

- *Basic information*：
  - Strapi Cloud 项目当前 environment 的名称。名称在创建 environment 时确定，之后无法修改；
  - environment 的 Node version，可在此修改项目使用的 Node version；
  - environment 对应 app 的 internal name，可用于调试和支持。
- *Connected branch*：修改 environment 使用的 GitHub repository branch，同时可以启用或禁用 “deploy on push”；
- *Environment data*：从同一项目的其他 environment 传输数据，或者在保留 settings 的前提下清除当前 environment 的全部数据与 assets；
- *Danger zone*：永久删除额外 environment。

#### Modifying Node version

**Original:** The environment's Node version is based on the one chosen at the creation of the project, through the advanced settings. It is possible to switch to another Node version afterwards, for any environment.

**中文译文:** Environment 的 Node version 最初来自创建项目时 advanced settings 中的选择。项目创建后，任意 environment 都可以切换到其他 Node version。

**Original:**
1. In the *Basic information* section of the *Configuration* tab, click on the *Node version*'s edit button.
2. Using the *Node version* drop-down in the dialog, click on the version of your choice.
3. Click on **Save**, or **Save & deploy** if you want the changes to take effect immediately.

**中文译文:**
1. 在 *Configuration* 标签页的 *Basic information* 区域点击 *Node version* 的编辑按钮；
2. 在对话框的 *Node version* 下拉菜单中选择目标版本；
3. 点击 **Save** 保存，或者点击 **Save & deploy** 立即应用并 deployment。

**Original:** Ensure the Node version configured in your Strapi project matches the Node version shown in your project’s dashboard before deploying.

**中文译文:** Deployment 前，请确保 Strapi 项目配置的 Node version 与项目 dashboard 中显示的 Node version 一致。

**Original:** The package manager version is not set in the project settings. During the build, Strapi Cloud detects which package manager to use from your project's lockfile, defaulting to npm.

- For `yarn` and `pnpm`, Corepack is enabled in the build environment, so the version pinned in your `package.json` `packageManager` field is honored automatically. If no version is pinned, Corepack's bundled default version is used.
- `npm` is not managed by Corepack: it uses the version bundled with the selected Node.js release.

**中文译文:** Package manager 版本不会在 project settings 中设置。构建期间，Strapi Cloud 会根据项目的 lockfile 检测所使用的 package manager；如果无法判断，则默认使用 npm。

- 对 `yarn` 和 `pnpm`，build environment 已启用 Corepack，因此会自动使用 `package.json` 的 `packageManager` 字段中锁定的版本。如果没有锁定版本，则使用 Corepack 自带的默认版本；
- `npm` 不由 Corepack 管理，而是使用所选 Node.js release 自带的 npm 版本。

#### Editing Git branch

**Original:**
1. In the *Edit branch* dialog, edit the available settings. Note that the branch can be edited for all environments at the same time via the project settings.

| Setting name | Instructions |
| --- | --- |
| Selected branch | (mandatory) Choose a branch from the drop-down list. |
| Base directory | Write the path of the base directory in the textbox. |
| Deploy the project on every commit pushed to this branch | Tick the box to automatically trigger a new deployment whenever a new commit is pushed to the selected branch. Untick it to disable the option. |

2. Click on the **Save & deploy** button for the changes to take effect.

**中文译文:**
1. 在 *Edit branch* 对话框中修改以下设置。也可以通过项目级 settings 一次性修改所有 environments 的 branch：

| 设置名称 | 说明 |
| --- | --- |
| Selected branch | （必填）从下拉列表选择 branch。 |
| Base directory | 在文本框中填写 base directory 路径。 |
| Deploy the project on every commit pushed to this branch | 勾选后，每当有新 commit 推送到所选 branch 时自动触发 deployment；取消勾选即可关闭。 |

2. 点击 **Save & deploy** 使变更生效。

#### Transferring data between environments

**Original:** The data transfer feature allows you to transfer the entire CMS content (database and assets) from one environment to another within the same Strapi Cloud project. This is useful for testing changes in a secondary environment with up-to-date production data, or for preparing and staging content in a secondary environment before taking it to production.

**中文译文:** Data transfer 功能可以在同一个 Strapi Cloud 项目的两个 environments 之间传输完整 CMS 内容，包括 database 与 assets。这适合将最新 production 数据复制到 secondary environment 中测试变更，也适合先在 secondary environment 准备和 staging 内容，再将其带到 production。

**Original:** Transferring data between environments currently comes with the following limitations:

- You can only transfer toward a secondary environment (not the production environment).
- Only project owners can initiate and manage ongoing transfers.
- Transfers cannot be initiated on projects that are suspended.

**中文译文:** 当前 environment data transfer 存在以下限制：

- 只能向 secondary environment 传输，不能以 Production environment 为目标；
- 只有 project owner 可以发起和管理正在进行的 transfer；
- suspended 状态的项目不能发起 transfer。

**Original:** Transferring data to an environment will permanently overwrite all existing data and assets in the target environment. The source environment's data remains unaffected, and its CMS can be accessed during the transfer. Environment settings (such as variables and domains) are not affected by the transfer.

**中文译文:** **Data transfer 是破坏性操作。** 向某个 environment 传输数据会永久覆盖目标 environment 现有的全部数据与 assets。Source environment 的数据不会受到影响，并且 transfer 期间仍可访问其 CMS。Environment settings（例如 variables 和 domains）不会被 transfer 修改。

**Original:** To transfer data to a secondary environment:

1. Create and deploy both the source and target environments.
2. In the *Environment data* section of the *Configuration* tab, click on the **Import data** button.
3. In the modal that opens, select the source environment from the drop-down list. Only fully created and deployed environments are available as sources.
4. Click on **Import data** to proceed, and follow the steps to confirm the transfer.
5. Once initiated, you will be redirected to the environment's dashboard where you can monitor the transfer's progress. Once the transfer is completed, the dashboard will refresh, showing both the ongoing and historic deployments.

**中文译文:** 向 secondary environment 传输数据：

1. 创建并完成 source environment 与 target environment 的 deployment；
2. 在 *Configuration* 标签页的 *Environment data* 区域点击 **Import data**；
3. 在弹出的 modal 中通过下拉列表选择 source environment。只有已经完整创建并成功 deployment 的 environments 才能作为 source；
4. 点击 **Import data** 并按后续步骤确认 transfer；
5. 发起后会跳转到 environment dashboard，可在其中查看 transfer 进度。完成后 dashboard 会刷新，并同时显示当前与历史 deployments。

**Original:** The CMS of the target environment will be inaccessible whilst the transfer is ongoing. You can cancel an ongoing transfer, but this will leave the target environment empty. If an error occurs during the transfer, you will have the option to retry or cancel.

**中文译文:** Transfer 进行期间，target environment 的 CMS 无法访问。可以取消正在执行的 transfer，但取消后 target environment 会处于空数据状态。如果 transfer 发生错误，可以选择 Retry 或 Cancel。

#### Clearing and deleting environments

**Original:** You can clear database content and assets from any environment, including the production environment, or permanently delete additional environments. The default production environment cannot be deleted.

**中文译文:** 可以清除任意 environment（包括 Production environment）中的 database 内容和 assets，也可以永久删除额外 environments。默认 Production environment 不能删除。

**Original:** On the Business plan, you cannot delete the included secondary environment. You can, however, clear its content.

**中文译文:** 在 Business plan 中，方案自带的 secondary environment 不能删除，但可以清空其内容。

**Original:** Clearing and deleting are permanent and only available to the project owner. You cannot initiate an environment clearing while the project is suspended.

**中文译文:** Clear 和 Delete 都是永久操作，并且仅 project owner 可以执行。项目处于 suspended 状态时，不能发起 environment clearing。

##### Clearing an environment

**Original:** Clearing an environment will permanently delete all its existing data and assets. Environment settings (such as variables and domains) are not affected by the clearing.

**中文译文:** **Clearing environment 是破坏性操作。** 它会永久删除该 environment 现有的全部数据和 assets，但不会影响 variables、domains 等 environment settings。

**Original:** To clear an environment:

1. In the project settings, select the environment then open the *Configuration* tab.
2. In the *Environment data* section, click **Clear environment**.
3. In the confirmation dialog, type the environment name, then confirm to start clearing. You are redirected to the environment dashboard, where you can follow the progress.

**中文译文:** 清空 environment：

1. 在 project settings 中选择目标 environment，然后打开 *Configuration* 标签页；
2. 在 *Environment data* 区域点击 **Clear environment**；
3. 在确认对话框中输入 environment name 并确认开始清理。之后会跳转到 environment dashboard，可在其中查看进度。

**Original:** While clearing is in progress:

- The environment CMS is not available.
- You cannot trigger a deployment or view the logs for that environment.
- Plan upgrade, plan downgrade and setting changes that require a deployment are temporarily unavailable.

If clearing fails, click **Retry** on the environment dashboard to run the operation again.

**中文译文:** Clearing 进行期间：

- environment CMS 不可用；
- 无法为该 environment 触发 deployment 或查看 logs；
- Plan upgrade、plan downgrade，以及需要 deployment 的 setting changes 会暂时不可用。

如果 clearing 失败，可以在 environment dashboard 点击 **Retry** 重新执行。

##### Deleting an environment

**Original:**
1. In the *Danger zone* section of the *Configuration* tab, click on the **Delete environment** button.
2. Write in the textbox your *Environment name*.
3. Click on the **Delete environment** button to confirm the deletion.

**中文译文:**
1. 在 *Configuration* 标签页的 *Danger zone* 区域点击 **Delete environment**；
2. 在文本框中输入 *Environment name*；
3. 再次点击 **Delete environment** 确认删除。

### Backups

**Original:** The *Backups* tab informs you of the status and date of the latest backup of your Strapi Cloud projects. The databases associated with all existing Strapi Cloud projects are indeed automatically backed up (weekly for Pro plans and daily for Business plans). Backups are retained for a 28-day period. Additionally, you can create a single manual backup.

**中文译文:** *Backups* 标签页显示 Strapi Cloud 项目最近一次 backup 的状态和日期。现有 Strapi Cloud 项目的 database 会自动备份：Pro plan 每周一次，Business plan 每日一次。Backups 保留 28 天。此外，还可以创建 1 份 manual backup。

**Original:**
- The backup feature is not available for Strapi Cloud projects on the Starter plan. You will need to upgrade to the Pro or Business plan to enable automatic backups and access the manual backup option.
- Backups include only the database of your default Production environment. Assets uploaded to your project and databases from any secondary environments are not included.
- The manual backup option becomes available shortly after the project’s first successful deployment.

**中文译文:**
- Starter plan 不提供 backup 功能。需要升级到 Pro 或 Business 才能启用 automatic backups，并使用 manual backup；
- Backup 仅包含默认 Production environment 的 database，不包含项目上传的 assets，也不包含任何 secondary environments 的 databases；
- 项目首次成功 deployment 后不久，manual backup 选项才会变为可用。

**Original:** For projects created before the release of the Backup feature in October 2023, the first backup will automatically be triggered with the next deployment of the project.

**中文译文:** 对于 2023 年 10 月 Backup 功能发布前创建的项目，首次 backup 会在项目下一次 deployment 时自动触发。

#### Creating a manual backup

**Original:** To create a manual backup, in the *Backups* section, click on the **Create backup** button.

The manual backup should start immediately, and restoration or creation of other backups will be disabled until the backup is complete.

**中文译文:** 若要创建 manual backup，在 *Backups* 区域点击 **Create backup**。Backup 会立即开始，在完成前，restore 以及创建其他 backups 的操作都会暂时禁用。

**Original:** When creating a new manual backup, any existing manual backup will be deleted. You can only have one manual backup at a time.

**中文译文:** 创建新的 manual backup 时，已有 manual backup 会被删除；同一时间只能保留 1 份 manual backup。

#### Restoring a backup

**Original:** If you need to restore a backup of your project:

1. In the *Backups* section, click on the **Restore backup** button.
2. In the dialog, choose one of the available backups (automatic or manual) of your project in the *Choose backup* drop-down.
3. Click on the **Restore** button of the dialog. Once the restoration is finished, your project will be back to the state it was at the time of the chosen backup. You will be able to see the restoration timestamp and the backup restored in the *Backups* tab.
4. The timestamp of the last completed restoration will be displayed to help you track when the project was last restored.

**中文译文:** 恢复项目 backup：

1. 在 *Backups* 区域点击 **Restore backup**；
2. 在对话框的 *Choose backup* 下拉列表中选择可用的 automatic 或 manual backup；
3. 点击 **Restore**。恢复完成后，项目会回到所选 backup 对应时间点的状态；*Backups* 标签页会显示 restoration timestamp 以及被恢复的 backup；
4. 页面还会显示最近一次完成 restoration 的 timestamp，便于追踪上次恢复时间。

#### Downloading a backup

**Original:** If you need to download a backup of your project:

1. In the *Backups* section, click on the **Download backup** button.
2. In the dialog, choose one of the available backups (automatic or manual) of your project in the *Choose backup* drop-down.
3. Click on the **Download** button of the dialog to download the chosen backup's archive file in `.sql` format.

**中文译文:** 下载项目 backup：

1. 在 *Backups* 区域点击 **Download backup**；
2. 在 *Choose backup* 下拉列表选择 automatic 或 manual backup；
3. 点击 **Download**，以 `.sql` 格式下载所选 backup 的 archive file。

**Original:** The backup file will include only the database of your default Production environment. It will not include assets or any other environment databases.

**中文译文:** Backup 文件只包含默认 Production environment 的 database，不包含 assets，也不包含其他 environments 的 databases。

### Domains

**Original:** The *Domains* tab enables you to manage domains and connect new ones.

**中文译文:** *Domains* 标签页用于管理已有 domains 和连接新的 domain。

**Original:** All existing domains for your Strapi Cloud project are listed in the *Domains* tab. For each domain, you can:

- see its current status:
  - Active: the domain is currently confirmed and active
  - Pending: the domain transfer is being processed, waiting for DNS changes to propagate
  - Failed: the domain change request did not complete as an error occurred
- click the edit button to access the settings of the domain
- click the delete button to delete the domain

**中文译文:** Strapi Cloud 项目的全部现有 domains 都会列在 *Domains* 标签页。对于每个 domain，可以：

- 查看当前状态：
  - Active：domain 已确认并处于 active 状态；
  - Pending：domain 变更正在处理，等待 DNS changes 完成传播；
  - Failed：domain change request 因发生错误而未能完成；
- 点击 edit 按钮进入该 domain 的 settings；
- 点击 delete 按钮删除该 domain。

#### Connecting a custom domain

**Original:** Default domain names are made of 2 randomly generated words followed by a hash. They can be replaced by any custom domain of your choice.

**中文译文:** 默认 domain name 由 2 个随机生成的单词和一个 hash 组成，可以替换为自定义 domain。

**Original:**
1. Click the **Connect new domain** button.
2. In the window that opens, fill in the following fields:

| Setting name | Instructions |
| --- | --- |
| Domain name | Type the new domain name (e.g. *custom-domain-name.com*) |
| Hostname | Type the hostname (i.e. address end-users enter in web browser, or call through APIs). |
| Target | Type the target (i.e. actual address where users are redirected when entering hostname). |
| Set as default domain | Tick the box to make the new domain the default one. |

3. Click on **Save & deploy** for the changes to take effect.

**中文译文:**
1. 点击 **Connect new domain**；
2. 在弹出的窗口中填写：

| 设置名称 | 说明 |
| --- | --- |
| Domain name | 输入新的 domain name，例如 `custom-domain-name.com`。 |
| Hostname | 输入 hostname，即终端用户在浏览器中输入或通过 APIs 调用的地址。 |
| Target | 输入 target，即用户访问 hostname 时最终被导向的实际地址。 |
| Set as default domain | 勾选后将新 domain 设置为默认 domain。 |

3. 点击 **Save & deploy** 使变更生效。

**Original:** To finish setting up your custom domain, in the settings of your domain registrar or hosting platform, please add the Target value (e.g., `proud-unicorn-123456af.strapiapp.com`) as a CNAME alias to the DNS records of your domain.

**中文译文:** 若要完成 custom domain 设置，需要在 domain registrar 或 hosting platform 的设置中，把 Target 值（例如 `proud-unicorn-123456af.strapiapp.com`）作为 CNAME alias 添加到该 domain 的 DNS records。

**Original:** When using custom domains, these domains do not apply to the URLs of uploaded assets. Uploaded assets keep the Strapi Cloud project-based URL.

This means that, if your custom domain is hosted at `https://my-custom-domain.com` and your Strapi Cloud project name is `my-strapi-cloud-instance`, API calls will still return URLs such as `https://my-strapi-cloud-instance.media.strapiapp.com/example.png`.

Media library queries over REST or GraphQL always return the project media domain on Strapi Cloud. If you move from a self-hosted project, media URLs will no longer match your own domain or CDN. Plan to use the absolute URLs returned by the API, or adjust your frontend to allow the Strapi Cloud media domain.

**中文译文:** 使用 custom domain 时，该 domain **不会应用到已上传 assets 的 URL**；上传的 assets 仍使用基于 Strapi Cloud 项目的 URL。

例如 custom domain 为 `https://my-custom-domain.com`，Strapi Cloud 项目名为 `my-strapi-cloud-instance`，API calls 仍可能返回 `https://my-strapi-cloud-instance.media.strapiapp.com/example.png` 这样的 URL。

在 Strapi Cloud 中，通过 REST 或 GraphQL 查询 Media Library 时始终返回项目的 media domain。如果项目从 self-hosted 迁移到 Strapi Cloud，media URLs 将不再与原有自定义 domain 或 CDN 一致。Frontend 应使用 API 返回的 absolute URLs，或者显式允许 Strapi Cloud media domain。

### Variables

**Original:** Environment variables are used to configure the environment of your Strapi application, such as the database connection.

**中文译文:** Environment variables 用于配置 Strapi application 的运行环境，例如 database connection。

**Original:** Custom variables are available to the Strapi server at runtime. Variables prefixed with `STRAPI_ADMIN_` are not exposed to the admin front end on Strapi Cloud.

**中文译文:** Custom variables 在 runtime 可供 Strapi server 使用。在 Strapi Cloud 中，以 `STRAPI_ADMIN_` 为前缀的 variables **不会暴露给 admin front end**。

**Original:** In the *Variables* tab are listed both the default and custom environment variables for your Strapi Cloud project. Each variable is composed of a *Name* and a *Value*.

**中文译文:** *Variables* 标签页会列出 Strapi Cloud 项目的 default 和 custom environment variables。每个 variable 都由 *Name* 与 *Value* 组成。

#### Managing environment variables

**Original:** Hovering on an environment variable, either default or custom, displays the following available options:

- **Show value** to replace the `*` characters with the actual value of a variable.
- **Copy to clipboard** to copy the value of a variable.
- **Actions** to access the Edit and Delete buttons.
  - When editing a default variable, the *Name* cannot be modified and the *Value* can only be automatically generated using the Generate value button. Don't forget to **Save**, or **Save & deploy** if you want the changes to take effect immediately.
  - When editing a custom variable, both the *Name* and *Value* can be modified by writing something new or by using the Generate value button. Don't forget to **Save**, or **Save & deploy** if you want the changes to take effect immediately.
  - When deleting a variable, you will be asked to confirm by selecting **Save**, or **Save & deploy** if you want the changes to take effect immediately.

**中文译文:** 将鼠标悬停在 default 或 custom environment variable 上时，会显示以下操作：

- **Show value**：将 `*` 替换为 variable 的实际值；
- **Copy to clipboard**：复制 variable value；
- **Actions**：打开 Edit 与 Delete：
  - 编辑 default variable 时，*Name* 不可修改，*Value* 只能通过 Generate value 自动生成。修改后点击 **Save**，或者点击 **Save & deploy** 立即应用；
  - 编辑 custom variable 时，*Name* 和 *Value* 都可以直接修改，也可以使用 Generate value。修改后点击 **Save**，或者点击 **Save & deploy** 立即应用；
  - 删除 variable 时，需要选择 **Save** 确认，或者选择 **Save & deploy** 立即应用并 deployment。

**Original:** Use the search bar to find more quickly an environment variable in the list!

**中文译文:** 可以使用 search bar 更快地在列表中查找 environment variable。

#### Creating custom environment variables

**Original:** Custom environment variables can be created for the Strapi Cloud project. Make sure to redeploy your project after creating or editing an environment variable.

**中文译文:** 可以为 Strapi Cloud 项目创建 custom environment variables。创建或编辑 environment variable 后，请确保重新 deployment 项目。

**Original:**
1. In the *Custom environment variables* section, click on the **Add variable** button.
2. Write the *Name* and *Value* of the new environment variable in the same-named fields. Alternatively, you can click on the Generate value icon to generate automatically the name and value.
3. (optional) Click on **Add another** to directly create one or more other custom environment variables.
4. Click on the **Save** button to confirm the creation of the custom environment variables. To apply your changes immediately, click on **Save & deploy**.

**中文译文:**
1. 在 *Custom environment variables* 区域点击 **Add variable**；
2. 在对应字段填写新 environment variable 的 *Name* 与 *Value*；也可以点击 Generate value 图标自动生成名称和值；
3. （可选）点击 **Add another**，继续创建一个或多个 custom environment variables；
4. 点击 **Save** 确认创建；如需立即应用变更，点击 **Save & deploy**。
