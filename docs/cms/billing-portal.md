# 📖 对照翻译：Billing portal

> Source: `docusaurus/docs/cms/billing-portal.md`  
> Upstream SHA: `8b8a60efb9438eda38c7d3833093268333bedd3b`

**Original:** The Strapi billing portal is where you can view all Strapi subscriptions and manage payment methods, billing details, and invoices. Only Growth subscriptions can be managed in the portal; Cloud and Enterprise subscriptions are view-only.

**中文译文:** Strapi billing portal 用于查看全部 Strapi subscriptions，并管理 payment methods、billing details 与 invoices。只有 Growth subscription 可以直接在 portal 中管理；Cloud 与 Enterprise subscription 在这里主要用于查看。

**Original:** The Strapi billing portal is where you view and manage billing for your Strapi subscriptions. For all subscriptions, you can update payment methods, edit billing details, and download invoices.

**中文译文:** [Strapi billing portal](https://billing.strapi.io) 是统一查看和管理 Strapi subscription billing 的入口。对于所有 subscriptions，都可以更新 payment method、修改 billing details 和下载 invoice。

**Original:** You can view all subscriptions in the portal, but only Growth subscriptions can be managed directly there. Cloud subscriptions are managed in the Strapi Cloud dashboard. Enterprise changes require contacting sales.

**中文译文:** Portal 中可以查看全部 subscriptions，但只有 Growth subscription 可以直接修改。Cloud subscription 需要在 [Strapi Cloud dashboard](/cloud/projects/settings#plans) 中管理；如需修改 Enterprise plan，需要联系 Strapi sales。

## Sign in

**Original:** To sign in:
1. Enter the email used at purchase or CLI authentication.
2. Enter the 6-digit code sent to your inbox.
3. If the email is linked to multiple billing accounts, select the account to manage.

**中文译文:** 登录 [billing portal](https://billing.strapi.io)：
1. 输入购买 subscription 或 CLI authentication 时使用的 email；
2. 输入发送到 inbox 的 6 位验证码；
3. 如果该 email 关联多个 billing accounts，选择要管理的 account。

## Subscriptions

**Original:** The Subscriptions tab displays all Strapi subscriptions. They are grouped as In trial, Active, Scheduled for cancellation, and Canceled.

**中文译文:** *Subscriptions* 标签页显示全部 Strapi subscriptions，并按状态分组：
- **In trial**：尚未转为付费的 trial；
- **Active**：正在生效的 subscription；
- **Scheduled for cancellation**：已安排在当前 billing period 结束时取消；
- **Canceled**：已经完全取消。

**Original:** Each subscription card shows plan name, product family, status, price, billing period, renewal/trial end date, and subscription ID. Cloud cards also show Cloud project name; Growth cards show the CMS project ID linked to the license.

**中文译文:** 每张 subscription card 会显示 plan name、product family、status、price、billing period（月 / 年）、renewal 或 trial end date，以及 subscription ID。Cloud subscription 还显示 Cloud project name；Growth subscription 则显示与 license 关联的 CMS project ID。

### Activating an in-trial Growth subscription

**Original:** Before activation, add a payment method and complete Billing details.

**中文译文:** 激活 trial Growth subscription 前，需要先在 *Payment methods* 添加 payment method，并填写完整 *Billing details*。

**Original:** 1. Click **Activate subscription**.
2. Set seat count and optionally include the SSO add-on.
3. Click **Continue** and review charges.
4. Click **Activate now**.

**中文译文:** 1. 在 *In trial* 区域点击 **Activate subscription**；
2. 在 *Manage subscription* modal 中设置 seat count，并选择是否包含 SSO add-on；
3. 点击 **Continue** 查看收费摘要；
4. 点击 **Activate now** 确认激活。

**Original:** Growth subscriptions must include at least 3 seats.

**中文译文:** Growth subscription 至少必须包含 3 个 seats。

### Changing seats and add-ons

**Original:** 1. Click **Manage subscription**.
2. Adjust seat count/add-ons.
3. Click **Continue** and review charges.
4. Click **Confirm**.

**中文译文:** 更新 active Growth subscription 的 seats 或 add-ons：
1. 点击 **Manage subscription**；
2. 调整 seat count 与 add-ons；
3. 点击 **Continue** 检查收费摘要；
4. 点击 **Confirm** 应用变更。

**Original:** Adding seats or enabling SSO is charged immediately on a prorated basis. CMS checks license updates at startup and every 12 hours, so seats can take up to 12 hours to appear; restart for faster application.

**中文译文:** 增加 seats 或启用 SSO add-on 时，会立即按比例收取费用。Strapi CMS instance 会在 startup 以及每 12 小时检查一次 license update，因此新增 seats 最多可能等待 12 小时才出现在 admin panel；如需更快生效，可以重启 Strapi instance。

**Original:** Removing seats or disabling SSO takes effect at next renewal. If adding seats and disabling SSO together, seats are charged immediately while SSO removal remains deferred.

**中文译文:** 减少 seats 或关闭 SSO add-on 会在下一次 renewal 生效，在此之前当前配置继续有效。如果同一次修改中既增加 seats 又关闭 SSO，seat increase 会立即收费，而 SSO removal 仍延迟到下一次 renewal。

### Canceling a Growth subscription

**Original:** 1. Click **Cancel subscription**.
2. Confirm cancellation. It takes effect at the end of the billing period, and can be undone while pending. A canceled subscription can also be reactivated later.

**中文译文:** 1. 点击 **Cancel subscription**；
2. 在 dialog 中点击 **Confirm** 安排取消。Cancellation 会在 billing period 结束时生效；等待期间可以撤销安排并恢复 subscription。即使 cancellation 已正式生效，也可以通过 subscription card 上的 **Reactivate** 重新激活。

## Payment methods

**Original:** The Payment methods tab manages cards used for subscriptions.

**中文译文:** *Payment methods* 标签页用于管理 subscription 使用的 payment cards。

### Adding a new card

**Original:** 1. Click **Add card**.
2. Enter card number, expiration date, CVV/CVC.
3. Optionally set as default.
4. Click **Save**.

**中文译文:** 1. 点击 **Add card**；
2. 输入 card number、expiration date 和 CVV/CVC；
3. （可选）勾选 **Set as default payment method**；
4. 点击 **Save**。

**Original:** The default card is used for all subscription transactions including add-ons and overages.

**中文译文:** Default card 会用于所有 subscription 相关交易，包括 add-ons 与 overages。

### Updating or removing a card

**Original:** Use the card menu to Set as default or Edit card. To remove a card, choose Remove card and confirm.

**中文译文:** 使用 card 的三点菜单可以 **Set as default**，或选择 **Edit card** 修改 card number、expiration date 和 CVV/CVC。删除时选择 **Remove card**，然后在 dialog 中确认。

**Original:** You cannot remove the default card. Removing a secondary card attached to subscriptions automatically cancels all subscriptions attached to that card.

**中文译文:** 不能删除 default card。如果 secondary card 已绑定 subscription（例如 Cloud subscription），删除该 card 会自动取消所有绑定到它的 subscriptions。

## Billing details

**Original:** Billing details contains account billing information. Required fields must be completed to activate a trial subscription.

**中文译文:** *Billing details* 用于查看和编辑 account billing information。要激活 trial subscription，必须填写其中所有 required fields。

**Original:** Taxes may be added based on billing address. EU/UK/Canada/India can be VAT-exempt with a valid VAT ID; US sales tax is based on state/address.

**中文译文:** 税费可能根据 billing address 加入 invoice。在欧盟、英国、加拿大和印度，提供有效 VAT ID 可以免除 VAT；美国 sales tax 根据所在州和地址计算。

## Invoices

**Original:** The Invoices tab displays all subscription invoices and their status.

**中文译文:** *Invoices* 标签页显示全部 Strapi subscription invoices 及其状态。

**Original:** Statuses:
- Paid: payment received, no action needed.
- Pending: invoice incomplete/not validated or payment requires fixing.
- Unpaid: payment failed and won't automatically retry.
- Voided: invoice canceled.

**中文译文:** Invoice status：
- **Paid**：已收到付款，invoice 可用，无需其他操作；
- **Pending**：invoice 尚未完成 / 验证，或者 payment 未成功、需要处理；
- **Unpaid**：payment 失败，并且不会自动重试；
- **Voided**：invoice 已取消。

**Original:** Click the download icon to download an invoice.

**中文译文:** 点击 download icon 可以下载 invoice。
