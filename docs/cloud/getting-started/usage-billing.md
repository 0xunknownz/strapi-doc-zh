# 📖 对照翻译：Cloud billing & usage

> Source: `docusaurus/docs/cloud/getting-started/usage-billing.md`  
> Upstream SHA: `e7aa1359d8e6c535792a4f646eb6fcb9ab0b3751`

**Original:** Cloud billing & usage

**中文译文:** Cloud 计费与用量

**Original:** Strapi Cloud offers three plans (Starter, Pro, and Business) with usage-based pricing that varies by API requests, asset storage, and bandwidth, plus overages charged monthly; projects may be suspended for unpaid invoices or plan violations.

**中文译文:** Strapi Cloud 提供 Starter、Pro 和 Business 3 种方案，并根据 API 请求数、Asset Storage 和 Asset Bandwidth 等用量计费；超额用量按月收费。若存在未支付账单或违反方案/服务条款等情况，项目可能会被暂停服务。

**Original:** This page contains general information related to the usage and billing of your Strapi Cloud account and projects.

**中文译文:** 本页面介绍 Strapi Cloud 账户和项目在用量与计费方面的通用信息。

**Original:** Strapi Cloud offers 3 plans: Starter, Pro, and Business. The table below summarizes Strapi Cloud usage-based pricing plans, for general features and usage:

**中文译文:** Strapi Cloud 提供 3 种方案：Starter、Pro 和 Business。下表汇总了这些按用量计费方案中的主要功能与资源额度，详细价格请参阅 [Pricing 页面](https://strapi.io/pricing-cloud)。

**Original:** 

| Feature | Starter | Pro | Business |
| --- | ---: | ---: | ---: |
| **Database Entries** | Unlimited* | Unlimited* | Unlimited* |
| **Asset Storage** | 50GB | 250GB | 1,000GB |
| **Asset Bandwidth (per month)** | 50GB | 500GB | 1,000GB |
| **API Requests (per month)** | 100,000 | 1,000,000 | 10,000,000 |
| **Backups** | N/A | Weekly | Daily |
| **Custom domains** | Included | Included | Included |
| **Environments** | N/A | 0 included (up to 99 extra) | 1 included (up to 99 extra) |
| **Emails (per month)** | Unlimited* | Unlimited* | Unlimited* |

**中文译文:**

| 功能 / 用量 | Starter | Pro | Business |
| --- | ---: | ---: | ---: |
| **Database Entries** | Unlimited* | Unlimited* | Unlimited* |
| **Asset Storage** | 50GB | 250GB | 1,000GB |
| **Asset Bandwidth（每月）** | 50GB | 500GB | 1,000GB |
| **API Requests（每月）** | 100,000 | 1,000,000 | 10,000,000 |
| **Backups** | N/A | 每周 | 每日 |
| **Custom domains** | 包含 | 包含 | 包含 |
| **Environments** | N/A | 默认不包含，可额外添加最多 99 个 | 包含 1 个，可额外添加最多 99 个 |
| **Emails（每月）** | Unlimited* | Unlimited* | Unlimited* |

**Original:** Additional information on usage and features:

- Database entries are the number of entries in your database.
- Asset storage is the amount of storage used by your assets.
- Asset bandwidth is the amount of bandwidth used by your assets.
- API requests are the number of requests made to your APIs. This includes requests to the GraphQL and REST APIs, excluding requests for file and media assets counted towards CDN bandwidth and storage. All API requests are counted towards your monthly usage, regardless of the response type.
- Backups refers to the automatic backups of Strapi Cloud projects.
- Custom domains refer to the ability to define a custom domain for your Strapi Cloud.
- Environments refers to the number of environments included in the plan on top of the default production environment.

**中文译文:** 关于用量与功能的补充说明：

- Database entries：数据库中的条目数量。
- Asset storage：项目资源文件所占用的存储空间。
- Asset bandwidth：资源文件产生的带宽用量。
- API requests：向项目 API 发起的请求数量，包括 GraphQL 和 REST API 请求；文件和媒体资源请求不计入 API Requests，而是计入 CDN bandwidth 与 storage。无论 API 返回什么类型的响应，所有 API 请求都会计入月度用量。
- Backups：Strapi Cloud 项目的自动备份功能，详见 [Backups 文档](/cloud/projects/settings#backups)。
- Custom domains：为 Strapi Cloud 项目设置自定义域名的能力，详见 [Custom domains](/cloud/projects/settings#connecting-a-custom-domain)。
- Environments：除默认 production environment 外，方案中额外包含的 environment 数量，详见 [Environments 文档](/cloud/projects/settings#environments)。

## Environments management

**Original:** Environments are isolated instances of your Strapi Cloud project. All projects have a default production environment, but other additional environments can be configured for projects on a Pro or Business plan, from the Environments tab of the project settings. There is no limit to the number of additional environments that can be configured for a Strapi Cloud project.

**中文译文:** Environments 是 Strapi Cloud 项目的相互隔离实例。所有项目都有一个默认 production environment；对于 Pro 或 Business 方案，还可以在项目设置的 *Environments* 标签页中配置额外 environment。Strapi Cloud 项目可配置的额外 environment 数量本身没有固定上限，具体方案包含数量及额外购买规则请以当前方案为准。

**Original:** The usage limits of additional environments are the same as for the project's production environment (e.g. an additional environment on the Pro plan will be limited at 250GB for asset storage, and overages will be charged the same way as for the production environment). Note however that the asset bandwidth and API calls are project-based, not environment-based, so these usage limits do not change even with additional environments.

**中文译文:** 额外 environment 的资源额度与项目 production environment 相同。例如，Pro 方案中的额外 environment，其 Asset Storage 上限同样为 250GB，超额用量也按照与 production environment 相同的方式计费。需要注意的是，Asset Bandwidth 和 API calls 是按**项目**统计，而不是按 environment 分别统计，因此即使增加 environment，这两项用量上限也不会随之增加。

## Billing

**Original:** Billing is based on the usage of your Strapi Cloud projects. Project plans and addons are either billed monthly or yearly, depending on your billing cycle, while overages are billed monthly. You can view your billing information in the Billing & Invoices tab of your project settings.

**中文译文:** Strapi Cloud 根据项目实际用量计费。项目方案和 add-ons 根据你选择的 billing cycle 按月或按年收费，而 overages 则统一按月计费。你可以在项目设置的 *Billing & Invoices* 标签页中查看计费信息。

### Taxes

**Original:** For billing addresses in the US, UK, Canada, India, and EU, local taxes may be added to your invoices. Tax amounts are calculated based on your billing address and VAT/Tax ID status, and are displayed during checkout and on invoices.

**中文译文:** 对于位于美国、英国、加拿大、印度和欧盟的账单地址，发票中可能会加入当地税费。税额根据 billing address 以及 VAT/Tax ID 状态计算，并会在结账页面和发票中显示。

**Original:** You can add or update your VAT/Tax ID from your Account Billing settings.

**中文译文:** 你可以在 [Account Billing](/cloud/account/account-billing) 设置中添加或更新 VAT/Tax ID。

### Overages

**Original:** If you exceed the limits of your plan for API Requests, Asset Bandwidth, or Asset Storage, you will be charged for the corresponding overages.

**中文译文:** 如果 API Requests、Asset Bandwidth 或 Asset Storage 超出当前方案额度，将针对超出的部分收取 overage 费用。

**Original:** For example, if you exceed the 500GB limit in asset bandwidth of the Pro plan, you will be charged for the excess bandwidth at the end of the current billing period or on project deletion. Overages are not prorated and are charged in full.

**中文译文:** 例如，如果 Pro 方案的 Asset Bandwidth 超过 500GB 上限，超出的带宽将在当前 billing period 结束时或项目被删除时计费。Overages 不按比例折算，而是按对应计费单位完整收费。

**Original:** Overages are charged monthly, according to the following rates:

| Feature | Rate |
| --- | --- |
| **API Requests** | $1.50 / 25k requests |
| **Asset Bandwidth** | $30.00 / 100GB |
| **Asset Storage** | $0.60 / GB per month |

**中文译文:** Overages 按月计费，当前费率如下：

| 项目 | 费率 |
| --- | --- |
| **API Requests** | $1.50 / 25k requests |
| **Asset Bandwidth** | $30.00 / 100GB |
| **Asset Storage** | $0.60 / GB / 月 |

### Project suspension

**Original:** Projects may end up in a Suspended state for various reasons, including unpaid invoices or violating Strapi Cloud's terms of service.

**中文译文:** 项目可能因为多种原因进入 **Suspended** 状态，包括存在未支付发票，或违反 Strapi Cloud 的 [terms of service](https://strapi.io/cloud-legal)。

**Original:** If your project is suspended, you will no longer be able to access the Strapi admin panel, nor trigger new deployments. A banner will appear in your project's dashboard, indicating the cause of the suspension. You will also be notified by email.

**中文译文:** 项目被暂停后，你将无法继续访问 Strapi 管理面板，也无法触发新的 deployment。项目 dashboard 中会显示一条 banner，说明暂停原因，同时你也会收到邮件通知。

#### Project suspension due to billing issues

**Original:** If you have unpaid invoices, the subscription of your project will automatically be canceled and the project suspended.

**中文译文:** 如果存在未支付发票，项目订阅会被自动取消，项目同时进入 Suspended 状态。

**Original:** To reactivate your project subscription:

1. Click the Pay now button in the project banner, or in Settings > Billing & Invoices.
2. Pay your overdue invoice(s) on the external payment page.
3. Wait up to 1 minute for your project to reactivate.

**中文译文:** 要重新激活项目订阅：

1. 点击项目 banner 中的 **Pay now**，或进入 *Settings > Billing & Invoices* 点击对应按钮。
2. 在外部支付页面结清逾期发票。
3. 最多等待约 1 分钟，让项目重新激活。

**Original:** If you do not resolve the issue within 30 days, your suspended project will be deleted and all its data will be permanently lost.

**中文译文:** 如果 30 天内仍未解决问题，被暂停的项目将被删除，其中全部数据也会永久丢失。

#### Project suspension for other reasons

**Original:** If your project was suspended for reasons other than unpaid invoice leading to subscription cancellation, you may not have the possibility to reactivate your project yourself. You should receive an email with instructions on how to resolve the issue. If you do not receive the email notification, please contact the Strapi Support platform.

**中文译文:** 如果项目因其他原因而被暂停，而不是因为未支付发票导致订阅取消，你可能无法自行重新激活项目。通常你会收到一封说明如何解决问题的邮件；如果没有收到通知，请联系 [Strapi Support platform](https://support.strapi.io/support/home)。

### Subscription cancellation

**Original:** If you want to cancel your Strapi Cloud subscription, you have 2 options:

- either delete your project,
- or completely delete your account.

**中文译文:** 如果希望取消 Strapi Cloud 订阅，有 2 种方式：

- 删除项目，详见 [Deleting Strapi Cloud project](/cloud/projects/settings#deleting-a-strapi-cloud-project)；
- 完全删除账户，详见 [Deleting Strapi Cloud account](/cloud/account/account-settings#deleting-strapi-cloud-account)。
