# 📖 对照翻译：Data Management

> Source: `docusaurus/docs/cms/features/data-management.md`  
> Upstream SHA: `0e8181d96e5d46725b386acd508ba1f9f15ff8a2`

**Original:** Data Management handles CLI-based import, export, and transfer of content between Strapi instances with partial configuration in the admin panel.

**中文译文:** Data Management 用于通过 CLI 在 Strapi instances 之间执行 import、export 和 transfer；部分配置则在 admin panel 中完成。

**Original:** The Data Management feature can be used to import, export, or transfer data. Data Management is CLI-based only, but is partly configured in the admin panel.

**中文译文:** Data Management 可用于 import、export 或 transfer data。实际操作只通过 CLI 执行，但部分前置配置需要在 admin panel 完成。

**Original:** Plan: Free feature. Role & permission: minimum "Access the transfer tokens settings page" in Roles > Settings - Transfer tokens. Activation: available and activated if a transfer salt is defined. Environment: Development & Production.

**中文译文:** 功能属性：Free feature；最低需要 *Roles > Settings - Transfer tokens* 中的 “Access the transfer tokens settings page” permission；定义 transfer salt 后功能可用并启用；Development 与 Production environment 均支持。

## Configuration

**Original:** Some configuration options are available in the admin panel, and some are handled via your Strapi project's code.

**中文译文:** Data Management 的部分配置在 admin panel 中完成，另一些配置通过 Strapi 项目代码处理。

### Admin panel settings

**Original:** A `transfer.token.salt` should be defined in the `config/admin` configuration file.

**中文译文:** 需要在 `config/admin` 中定义 `transfer.token.salt`，否则 transfer token 功能不会正常启用。

**Original:** Path to configure the feature: Settings > Global settings > Transfer Tokens.

**中文译文:** 配置路径：*Settings > Global settings > Transfer Tokens*。

**Original:** Transfer tokens allow users to authorize the `strapi transfer` CLI command.

**中文译文:** Transfer tokens 用于授权 `strapi transfer` CLI command。

**Original:** The Transfer Tokens interface lists each token's name, description, creation date, and last-use date. Administrators can edit a token's name, description, or type, regenerate it, or delete it.

**中文译文:** *Transfer Tokens* 界面会列出每个 token 的 name、description、creation date 和 last-use date。Administrator 可以编辑 token 的 name、description、type，执行 regenerate，或删除 token。

#### Creating a new transfer token

**Original:** 1. Click **Create new Transfer Token**.
2. Configure:

| Setting name | Instructions |
| --- | --- |
| Name | Write the token name. |
| Description | (optional) Write a description. |
| Token duration | Choose 7 days, 30 days, 90 days, or Unlimited. |
| Token type | Push, Pull, or Full Access. |

Push allows local-to-remote only, Pull allows remote-to-local only, and Full Access allows both.
3. Click **Save**. The new token is shown at the top with a copy button.

**中文译文:** 1. 点击 **Create new Transfer Token**。
2. 配置：

| 设置项 | 说明 |
| --- | --- |
| Name | 输入 token 名称。 |
| Description | （可选）输入描述。 |
| Token duration | 选择 7 days、30 days、90 days 或 Unlimited。 |
| Token type | 选择 Push、Pull 或 Full Access。 |

Push 仅允许 local → remote transfer；Pull 仅允许 remote → local；Full Access 同时允许两种方向。
3. 点击 **Save**。新 token 会显示在界面顶部，并提供 copy 按钮。

**Original:** For security reasons, Transfer tokens are shown only immediately after creation. After refresh or navigation, the token is hidden and will not be displayed again.

**中文译文:** 出于安全原因，Transfer token 只会在创建完成后立即显示。刷新页面或跳转到其他 admin panel 页面后，该 token 会被隐藏，之后不会再次显示。

#### Regenerating a Transfer token

**Original:** 1. Click the token's edit button.
2. Click **Regenerate**.
3. Confirm with **Regenerate**.
4. Copy the new token.

**中文译文:** 1. 点击 Transfer token 的 edit 按钮；
2. 点击 **Regenerate**；
3. 在 dialog 中再次点击 **Regenerate** 确认；
4. 复制新的 Transfer token。

### Code-based configuration

**Original:** A `transfer.token.salt` value must be defined in `config/admin`. If no value is defined, the feature is disabled. For increased security, put the salt in environment variables and import it with `env()`.

**中文译文:** 必须在 `config/admin` 中定义 `transfer.token.salt`，否则该功能会被禁用。为提高安全性，建议将 salt 放在 environment variable 中，并通过 `env()` 读取。

**Original code (kept unchanged):**

```js title="/config/admin.js"
module.exports = ({ env }) => ({
  // …
  transfer: { 
    token: { 
      salt: env('TRANSFER_TOKEN_SALT', 'anotherRandomLongString'),
    } 
  },
});
```

```ts title="/config/admin.ts"
export default ({ env }) => ({
  // …
  transfer: { 
    token: { 
      salt: env('TRANSFER_TOKEN_SALT', 'anotherRandomLongString'),
    } 
  },
});
```

**中文译文:** JavaScript 与 TypeScript 示例均保持原样。

**Original:** When exporting or transferring data, the admin panel configuration includes project settings such as logos. These logo files are embedded in the export and re-uploaded to the destination instance during import.

**中文译文:** Export 或 transfer data 时，admin panel configuration 也会包含项目 settings，例如 admin menu logo 与 authentication logo。Logo 文件会被嵌入 export，并在 import 时重新上传到 destination instance，从而保留 branding。

## Usage

**Original:** Data Management is CLI-based only. Import, export, or transfer commands must be executed from the terminal.

**中文译文:** Data Management 只通过 CLI 使用。Import、export 和 transfer commands 都必须在 terminal 中执行。

**Original:** The `strapi transfer` command verifies asset integrity using SHA-256 checksums by default when both instances support it. Use `--no-checksums` to disable verification. For large files or slow connections that trigger false stall detection, configure `transfer.remote.assetIdleTimeoutMs`.

**中文译文:** 当两端 instances 都支持时，`strapi transfer` 默认使用 SHA-256 checksums 验证 asset integrity。可通过 `--no-checksums` 关闭验证。对于大文件或慢速连接导致的误判 stall，可在 server configuration 中设置 `transfer.remote.assetIdleTimeoutMs`。

**Original:** Import — import data into a Strapi instance. Export — export data from a Strapi instance. Transfer — transfer data from one Strapi instance to another.

**中文译文:** Import：向 Strapi instance 导入数据；Export：从 Strapi instance 导出数据；Transfer：在两个 Strapi instances 之间传输数据。
