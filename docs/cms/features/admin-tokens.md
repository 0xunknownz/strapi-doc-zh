# 📖 对照翻译：Admin tokens

> Source: `docusaurus/docs/cms/features/admin-tokens.md`  
> Upstream SHA: `392b773b43842e4c111146ffbd3e3d87decdaa1b`

**Original:** Admin tokens authenticate programmatic access to the Strapi Admin API. Each token is scoped to a subset of its owner's permissions and is designed for automation workflows such as MCP agents, CI/CD pipelines, and scripts.

**中文译文:** Admin tokens 用于验证对 Strapi Admin API 的程序化访问。每个 token 的权限范围都受其 owner 自身权限限制，适合用于 MCP agents、CI/CD pipelines 和自动化脚本等工作流。

**Original:** Admin tokens allow automated clients to authenticate requests to the Strapi Admin API. For authenticating requests to the Content API, see API Tokens.

**中文译文:** Admin tokens 允许自动化 client 对 Strapi Admin API 请求进行 authentication。若要验证 Content API 请求，请参阅 [API Tokens](/cms/features/api-tokens)。

**Original:** Admin tokens and API tokens are strictly separated: each is rejected on the other's routes.

**中文译文:** Admin tokens 与 API tokens 严格隔离：两类 token 在对方的 routes 上都会被拒绝。

**Original:** Plan: Free feature. Role & permission: Activated by default for Super Admin. Each lower-level role needs an explicit permission grant in Roles > Settings - Admin tokens. Activation: Available and activated by default. Environment: Available in both Development & Production environment.

**中文译文:** 功能属性：这是 Free feature；Super Admin 默认拥有权限，其他较低级别 role 需要在 *Roles > Settings - Admin tokens* 中显式授权；功能默认可用并启用；Development 与 Production environment 均可使用。

## Configuration

**Original:** Admin tokens are configured entirely from the admin panel. No code-based configuration is specific to Admin tokens. The shared salt and encryption key that apply to all token kinds are set via `apiToken.salt` and `apiToken.secrets.encryptionKey` in your `/config/admin` file.

**中文译文:** Admin tokens 完全通过 admin panel 配置，没有只针对 Admin tokens 的独立 code-based configuration。所有 token 共用的 salt 与 encryption key 可在 `/config/admin` 中通过 `apiToken.salt` 和 `apiToken.secrets.encryptionKey` 配置，相关说明参见 [API tokens](/cms/features/api-tokens#code-based-configuration)。

**Original:** Path to configure the feature: Settings > Administration Panel > Admin Tokens.

**中文译文:** 配置路径：*Settings > Administration Panel > Admin Tokens*。

### Creating a new Admin token

**Original:** If you're not the Strapi instance's super admin, the super admin must have granted you permission to access the Admin tokens settings page and to create (generate) Admin tokens.

**中文译文:** 如果你不是该 Strapi instance 的 Super Admin，则必须由 Super Admin 授予你以下权限：访问 Admin tokens settings 页面，以及创建（生成）Admin tokens。详情参见 [RBAC > Configuring role's permissions](/cms/features/rbac#plugins-and-settings)。

**Original:** 1. Click on the **Create new Admin Token** button.
2. In the token creation form, configure the new Admin token:

| Setting name | Instructions |
| --- | --- |
| Name | Write the name of the token. |
| Description | (optional) Write a description for the token. |
| Token duration | Choose a duration: 7 days, 30 days, 90 days, or Unlimited. |

3. Define which admin actions this token can perform by browsing permission categories and enabling or disabling individual permissions.
4. Click **Save**. The new Admin token is displayed at the top of the interface with a copy button.

**中文译文:** 1. 点击 **Create new Admin Token**。
2. 在 token 创建表单中配置：

| 设置项 | 说明 |
| --- | --- |
| Name | 输入 token 名称。 |
| Description | （可选）输入 token 描述。 |
| Token duration | 选择 7 days、30 days、90 days 或 Unlimited。 |

3. 通过表单下方的权限分类设置该 token 可以执行的 admin actions，并用 checkbox 启用或禁用具体 permissions。
4. 点击 **Save**。新 Admin token 会显示在界面顶部，并提供 copy 按钮。

**Original:** Permissions that the current user does not hold appear disabled and cannot be selected. Conditions applied to the owner's role are shown as read-only and apply automatically to the token.

**中文译文:** 当前用户本身不具备的 permissions 会显示为 disabled，不能选择。Owner role 上已有的 conditions 会以 read-only 形式展示，并自动应用到 token。

**Original:** The plaintext token key is shown only once, immediately after creation or regeneration. The `admin.secrets.encryptionKey` configuration that makes Content API token keys persistently viewable does not apply to Admin tokens. Admin token keys are always restricted to the token owner, regardless of encryption configuration.

**中文译文:** Plaintext token key 只会在创建或 regeneration 后立即显示一次。用于让 Content API token key 持续可见的 `admin.secrets.encryptionKey` 配置**不适用于 Admin tokens**。无论 encryption 配置如何，Admin token key 都只对 token owner 开放。

### Managing Admin tokens

**Original:** Admin tokens have a dedicated settings page at Settings > Administration Panel > Admin Tokens. Admin tokens and API tokens are stored in the same database table (differentiated by a `kind` field) but are managed through independent interfaces in the admin panel.

**中文译文:** Admin tokens 有独立 settings 页面：*Settings > Administration Panel > Admin Tokens*。Admin tokens 与 API tokens 存储在同一 database table 中，通过 `kind` 字段区分，但在 admin panel 中由不同界面独立管理。

**Original:** The Admin Tokens page displays an Owner column showing the display name of each token's owner. Any user with access to the Admin Tokens settings page can view Admin tokens. A token can only be edited or deleted by its owner or a super-admin.

**中文译文:** Admin Tokens 页面包含 **Owner** 列，显示各 token owner 的 display name。任何拥有该 settings 页面访问权限的用户都可以查看 Admin tokens，但只有 token owner 或 Super Admin 可以编辑或删除 token。

**Original:** When a super-admin views an Admin token owned by another user, a read-only Owner field appears in the token details panel. The permissions panel shows only the checkboxes within the token owner's permission scope, not the super-admin's unrestricted access.

**中文译文:** 当 Super Admin 查看其他用户拥有的 Admin token 时，token details 中会显示 read-only 的 **Owner** 字段。Permissions 面板展示的是 token owner 权限范围内的 checkbox，而不是 Super Admin 自身无限制的权限范围。

**Original:** Removing a permission from a role causes Admin tokens owned by users of that role to have the corresponding permission deleted automatically.

**中文译文:** 如果从某个 role 中移除 permission，则该 role 用户所拥有的 Admin tokens 会自动删除对应 permission。

**Original:** If the token owner's account is deleted, all Admin tokens owned by that user are automatically deleted with their associated permissions. There is no recovery path. If the owner's account is deactivated or blocked, requests authenticated with that owner's Admin token are rejected, but re-activating or unblocking the owner restores token functionality.

**中文译文:** 如果 token owner 的账户被删除，该用户拥有的所有 Admin tokens 及其关联 permissions 都会自动删除，无法恢复。若 owner 账户只是被 deactivated 或 blocked，则使用其 Admin token authentication 的请求会被拒绝；重新启用或解除封禁 owner 后，token 功能会恢复。

#### Regenerating an Admin token

**Original:** The **Regenerate** button is only visible to the token's owner. Other users, including super-admins, do not see this button for tokens they do not own.

**中文译文:** **Regenerate** 只对 token owner 可见。其他用户即使是 Super Admin，也不会在不属于自己的 token 上看到该按钮。

**Original:** To regenerate an Admin token:
1. Click the Admin token's edit button.
2. Click **Regenerate**.
3. Confirm with **Regenerate** in the dialog.
4. Copy the new Admin token shown at the top of the interface.

**中文译文:** Regenerate Admin token：
1. 点击 Admin token 的 edit 按钮；
2. 点击 **Regenerate**；
3. 在 dialog 中再次点击 **Regenerate** 确认；
4. 复制界面顶部显示的新 Admin token。

## Usage

**Original:** Using Admin tokens allows executing a request on Strapi's admin routes as an authenticated user.

**中文译文:** 使用 Admin tokens，可以以 authenticated user 身份请求 Strapi 的 admin routes。

**Original:** Admin tokens can be helpful to give access to people or applications without managing a user account, for instance to connect an MCP server or a CI/CD pipeline.

**中文译文:** Admin tokens 适合在不单独管理 user account 的情况下，为人员或应用提供访问能力，例如连接 MCP server 或 CI/CD pipeline。

**Original:** When performing a request to Strapi's admin routes, the Admin token should be added to the request's `Authorization` header with the following syntax: `bearer your-admin-token`.

**中文译文:** 请求 Strapi admin routes 时，应将 Admin token 写入 request 的 `Authorization` header，格式为：`bearer your-admin-token`。

**Original:** Never expose Admin tokens in client-side code. Store them in a secrets manager or environment variable.

**中文译文:** 不要在 client-side code 中暴露 Admin tokens。请将其保存在 secrets manager 或 environment variable 中。
