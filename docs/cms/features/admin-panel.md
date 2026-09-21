# 📖 对照翻译：Administration panel

> Source: `docusaurus/docs/cms/features/admin-panel.md`  
> Upstream SHA: `769240cfa2bcfb7d9f9cd6e9b6be874f397479ae`

**Original:** The admin panel acts as Strapi’s back office for managing content types, entries, and both administrator and end-user accounts. This documentation gives an overview of the admin panel before focusing on profile settings that manage interface language and mode, login and personal information, and logo for branding.

**中文译文:** Admin panel 是 Strapi 的后台管理界面，用于管理 content types、entries，以及 administrator 与 end-user accounts。本页先介绍 admin panel 的整体结构，再说明 profile settings，包括界面语言与模式、登录与个人信息，以及 branding logo 等设置。

**Original:** The admin panel is the back office of your Strapi application. From the admin panel, you can manage content-types and their content, and manage both administrators and end users.

**中文译文:** Admin panel 是 Strapi application 的后台。你可以在这里管理 content-types 及其实际内容，也可以管理 administrators 和 end users。

**Original:** You can create your own widgets to customize the admin panel homepage. You can also resize, reorder, delete, and restore widgets.

**中文译文:** 可以通过 [自定义 widgets](/cms/admin-panel-customization/homepage) 调整 admin panel 首页。Widget 支持 Resize、Reorder、Delete 和 Restore；相关控制会在鼠标悬停到 widget 或 widget 之间时出现。

## Overview

**Original:** Development, Staging or Production Environment can change which features are available. Some features are only available in development.

**中文译文:** Development、Staging 和 Production environment 会影响界面与功能可用性。部分功能仅在 Development environment 可用；可通过文档中的 Identity Cards 判断具体环境支持情况。

**Original:** Some features or limits depend on the Community Edition, Growth plan, or Enterprise plan.

**中文译文:** 部分功能或使用上限取决于应用使用的是免费 Community Edition、Growth plan 还是 Enterprise plan。文档中会使用 Growth / Enterprise badges 标记。

**Original:** Roles and Permissions can restrict access to features and content.

**中文译文:** Roles 与 Permissions 会限制用户能够访问的功能与内容。详情参阅 [RBAC](/cms/features/rbac)。

**Original:** Some incoming features are available behind future flags for early community feedback.

**中文译文:** 部分尚未面向全部用户正式发布的新功能会通过 future flags 提前开放，以收集社区反馈。相关页面会带有 FeatureFlag badge，详情参阅 [Feature flags](/cms/configurations/features#enabling-a-future-flag)。

## Configuration

**Original:** Path to configure the admin panel: Account name or initials (bottom left) > Profile.

**中文译文:** 配置路径：主导航左下角的 account name 或 initials > **Profile**。

**Original:** New administrators should make sure their profile is configured. Profile settings allow editing name, username, email, password, interface language, and interface mode.

**中文译文:** 新 administrator 建议先完善 profile。这里可以修改 name、username、email、password，并选择 interface language 和 interface mode。

**Original:** More configuration and customization options are available through code-based configuration and Admin panel customization.

**中文译文:** 更深入的配置可参阅 [Code-based configuration](/cms/configurations/admin-panel) 与 [Admin panel customization](/cms/admin-panel-customization)。

### Modifying profile information

**Original:** 1. Go to the Profile section.
2. Fill in First name, Last name, Email, and optional Username.
3. Click **Save**.

**中文译文:** 1. 打开 profile 的 *Profile* 区域；
2. 填写 First name、Last name、Email，以及可选 Username；
3. 点击 **Save**。

### Changing account password

**Original:** 1. Go to the Change password section.
2. Fill in Current password, Password, and Password confirmation.
3. Click **Save**.

**中文译文:** 1. 打开 profile 中的 *Change password* 区域；
2. 填写 Current password、新 Password 和 Password confirmation；
3. 点击 **Save**。可以点击 eye 图标显示 password。

### Choosing interface language

**Original:** In the Experience section, select your preferred language with the Interface language dropdown. This choice applies only to your account.

**中文译文:** 在 profile 的 *Experience* 区域，通过 *Interface language* 下拉列表选择界面语言。该设置只影响当前账户；同一 application 的其他 admin users 可以选择不同语言。

### Choosing interface mode

**Original:** By default, interface mode follows the browser's mode. You can manually choose Light Mode or Dark Mode in the Experience section. This choice applies only to your account.

**中文译文:** 默认情况下，interface mode 跟随 browser mode。也可以在 *Experience* 中通过 *Interface mode* 手动选择 Light Mode 或 Dark Mode；该选择仅影响当前账户。

### Resetting guided tour

**Original:** Use Reset guided tour in the Guided tour section to make the homepage guided tour available again.

**中文译文:** 在 profile 的 *Guided tour* 区域点击 **Reset guided tour**，可以重新启用 admin panel 首页的引导流程。

### Customizing the logo

**Original:** Path: Settings > Global settings > Overview. The default Strapi logos in the main navigation and authentication pages can be replaced.

**中文译文:** 配置路径：*Settings > Global settings > Overview*。可以替换 Strapi application 主导航和 authentication pages 上显示的默认 Strapi logo。

**Original:** 1. Click the upload area for Menu logo or Auth logo.
2. Upload a logo by file browser, drag & drop, or URL. The logo should be no larger than 750x750px.
3. Click **Upload logo**.
4. Click **Save**.

**中文译文:** 1. 点击 *Menu logo* 或 *Auth logo* 的 upload area；
2. 通过文件选择、drag & drop 或 URL 上传 logo，尺寸不应超过 750x750px；
3. 点击 **Upload logo**；
4. 点击右上角 **Save**。

**Original:** Uploaded logos can be replaced or reset. Logos uploaded through the admin panel override logos configured in files.

**中文译文:** 上传后可以替换或 reset logo。通过 admin panel 上传的 logo 优先级高于 configuration files 中设置的 logo。程序化自定义方式参见 [Admin panel customization](/cms/admin-panel-customization/logos)。

## Usage

**Original:** To access the admin panel, the Strapi application must be running and you must know the admin URL, for example `api.example.com/admin`.

**中文译文:** 要访问 admin panel，Strapi application 必须已启动，并且需要知道 admin URL，例如 `api.example.com/admin`。

**Original:** 1. Go to the admin panel URL.
2. Enter credentials.
3. Click **Login**.

**中文译文:** 1. 打开 admin panel URL；
2. 输入 credentials；
3. 点击 **Login**，登录成功后会进入 admin panel 首页。

**Original:** If you prefer or are required to log in through SSO, see the Single Sign-On documentation.

**中文译文:** 如果希望或必须通过 SSO provider 登录，请参阅 [Single Sign-On](/cms/features/sso)。
