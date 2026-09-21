# 📖 对照翻译：Single Sign-On (SSO)

> Source: `docusaurus/docs/cms/features/sso.md`  
> Upstream SHA: `241ead0f53f2069b8f6d48d0768085a6765652d1`

**Original:** Single Sign-On (SSO) lets administrators authenticate via identity providers such as Azure AD instead of local passwords.

**中文译文:** Single Sign-On（SSO）允许 administrator 通过 Azure AD 等 identity provider 完成 authentication，而不使用本地 password。

**Original:** The SSO feature can be enabled on a Strapi application to allow administrators to authenticate through an identity provider such as Microsoft Azure Active Directory.

**中文译文:** 可以在 Strapi application 中启用 SSO，让 administrators 通过 Microsoft Azure Active Directory 等 identity provider 登录。

**Original:** Plan: CMS Enterprise plan, or SSO add-on with CMS Growth. Role & permission: Read & Update permissions in Roles > Settings - Single Sign-On. Activation: disabled by default. Environment: Development & Production.

**中文译文:** 功能属性：需要 CMS Enterprise plan，或在 CMS Growth plan 上购买 SSO add-on；需要 *Roles > Settings - Single Sign-On* 中的 Read 与 Update permissions；默认关闭；Development 与 Production environment 均支持。

## Configuration

**Original:** General SSO settings are available in the admin panel, and additional SSO providers can be configured through your Strapi project's code.

**中文译文:** SSO 的通用设置可以在 admin panel 中配置；额外的 SSO providers 则通过 Strapi 项目代码配置。

### Admin panel settings

**Original:** Path: Global settings > Single Sign-On.

**中文译文:** 配置路径：*Global settings > Single Sign-On*。

**Original:** Configure:

| Setting name | Instructions |
| --- | --- |
| Auto-registration | True lets SSO create a new Strapi administrator when no existing account matches; False requires accounts to be created manually first. |
| Default role | Role assigned by default to auto-registered SSO administrators. |
| Local authentication lock-out | Roles for which local authentication is disabled. Locked-out users must use SSO and cannot change or reset their password. |

**中文译文:** 配置项：

| 设置项 | 说明 |
| --- | --- |
| Auto-registration | 设为 True 时，如果 SSO login 没有匹配到已有 Strapi administrator account，会自动创建新 administrator；设为 False 时，需要事先手动创建账户。 |
| Default role | 通过 SSO 自动注册的 administrator 默认获得的 role。 |
| Local authentication lock-out | 禁用 local authentication 的 roles。被 lock-out 的用户必须通过 SSO 登录，并且不能修改或 reset password。 |

**Original:** Click **Save**.

**中文译文:** 配置完成后点击 **Save**。

**Original:** Do not select Super Admin for Local authentication lock-out. Otherwise you may accidentally lock yourself out of the admin panel. If this happens, temporarily disable SSO, log in with username/password, remove Super Admin from the lock-out list, then re-enable SSO.

**中文译文:** **不要**在 *Local authentication lock-out* 中选择 Super Admin，否则可能把自己完全锁在 admin panel 之外。如果已经发生，可临时关闭 SSO，使用 username/password 登录，移除 lock-out list 中的 Super Admin，再重新启用 SSO。

### Code-based configuration

**Original:** SSO configuration lives in the `/config/admin` file. Use the dedicated guide to configure additional sign-in and sign-up methods.

**中文译文:** SSO code-based configuration 位于 `/config/admin`。如需配置额外 sign-in / sign-up methods，请参阅 [How to configure SSO providers](/cms/configurations/guides/configure-sso)。

## Usage

**Original:** To access the admin panel through an SSO provider:
1. Go to the admin panel URL.
2. Click the provider logo at the bottom of the login form. If it is not visible, open the full provider list.
3. You are redirected to the provider's login page to authenticate.

**中文译文:** 通过 SSO provider 访问 admin panel：
1. 打开 Strapi application 的 admin panel URL；
2. 点击 login form 底部目标 provider 的 logo。如果没有显示，打开完整 provider list；
3. 页面会跳转到 provider 自己的 login page，完成 authentication。
