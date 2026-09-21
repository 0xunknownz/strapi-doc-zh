# 📖 对照翻译：Cloud account billing & invoices

> Source: `docusaurus/docs/cloud/account/account-billing.md`  
> Upstream SHA: `8ca30521b893de86605c08337cd047d59467712c`

**Original:** Cloud account billing & invoices

**中文译文:** Cloud 账户计费与发票

**Original:** Billing details and invoices are managed on the Profile page, where payment methods are updated and invoice history is available.

**中文译文:** Billing details 与 invoices 都在 *Profile* 页面中管理；你可以在这里更新 payment method，并查看 invoice history。

**Original:** Through the *Profile* page, accessible by clicking on your profile picture on the top right hand corner of the interface then clicking on **Profile**, you can access the *Billing* and *Invoices* tabs.

**中文译文:** 点击界面右上角的 profile picture，再点击 **Profile**，即可进入 *Profile* 页面，并访问 *Billing* 与 *Invoices* 标签页。

## Account billing

**Original:** The *Billing* tab displays and enables you to modify the billing details and payment method set for the account.

**中文译文:** *Billing* 标签页用于查看和修改账户的 billing details 与 payment method。

**Original:** The *Payment method* section of the *Billing* tab allows you to manage the credit cards that can be used for the Strapi Cloud projects. The *Billing details* section requires to be filled in, at least for the mandatory fields, as this information will be the default billing details for all Strapi Cloud projects related to your account.

**中文译文:** *Billing* 标签页中的 *Payment method* 区域用于管理可供 Strapi Cloud 项目使用的信用卡。*Billing details* 至少必须填写全部必填字段，因为这些信息会作为该账户下所有 Strapi Cloud 项目的默认 billing details。

### Adding a new credit card

**Original:** 1. In the *Payment method* section of the *Billing* tab, click on the **Add card** button.

**中文译文:** 1. 在 *Billing* 标签页的 *Payment method* 区域点击 **Add card**。

**Original:** 2. Fill in the following fields:

| Field name | Description |
| --- | --- |
| Card Number | Write the number of the credit card to add as payment method. |
| Expires | Write the expiration date of the credit card. |
| CVC | Write the 3-numbers code displayed at the back of the credit card. |

**中文译文:** 2. 填写以下字段：

| 字段 | 说明 |
| --- | --- |
| Card Number | 输入要作为 payment method 的信用卡卡号。 |
| Expires | 输入信用卡有效期。 |
| CVC | 输入信用卡背面的 3 位 CVC。 |

**Original:** 3. Click on the **Save** button.

**中文译文:** 3. 点击 **Save**。

**Original:** The first credit card to be added as payment method for the account will by default be the primary one. It is however possible to define another credit card as primary by clicking on the three dots icon, then **Switch as primary**.

**中文译文:** 添加到该账户的第一张信用卡默认会成为 primary card。也可以点击其他信用卡的三点菜单，然后选择 **Switch as primary**，将其设为新的 primary card。

### Deleting a credit card

**Original:** To remove a credit card from the list of payment methods for the account:

1. Click on the three dots icon of the credit card you wish to delete.
2. Click **Remove card**. The card is immediately deleted.

**中文译文:** 若要从账户的 payment methods 中删除信用卡：

1. 点击目标信用卡的三点菜单；
2. 点击 **Remove card**。该卡会立即被删除。

**Original:** You cannot delete the primary card as at least one credit card must be available as payment method, and the primary card is by default that one. If the credit card you wish to delete is currently the primary card, you must first define another credit card as primary, then delete it.

**中文译文:** 不能直接删除 primary card，因为账户必须至少保留一张可用作 payment method 的信用卡，而 primary card 默认承担这一角色。如果要删除的卡当前是 primary card，需要先把另一张信用卡设置为 primary，再删除原卡。

## Account invoices

**Original:** The *Invoices* tab displays the complete list of invoices for all your Strapi Cloud projects.

**中文译文:** *Invoices* 标签页会显示账户下所有 Strapi Cloud 项目的完整发票列表。

**Original:** Invoices are also available per project. In the *Settings > Billing & Invoices* tab of any project, you will find the invoices for that project only.

**中文译文:** 也可以按项目查看 invoices。在任意项目的 *Settings > Billing & Invoices* 标签页中，只会显示该项目自身的发票。详情请参阅 [对应文档](/cloud/projects/settings#billing--invoices)。
