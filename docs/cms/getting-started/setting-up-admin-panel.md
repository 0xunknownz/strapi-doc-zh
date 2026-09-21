# 📖 对照翻译：Setting up the admin panel

> Source: `docusaurus/docs/cms/getting-started/setting-up-admin-panel.md`  
> Upstream SHA: `cad74376187bec4bfea3b090a9f955064815b339`

**Original:** The admin panel is where you manage content-types, content, and users. Access it via the app URL, optionally using SSO, then configure your administrator profile including name, email, language, and password.

**中文译文:** Admin panel 是管理 content-types、内容和用户的后台界面。你可以通过应用 URL 访问它，也可以在启用后使用 SSO 登录；进入后可配置 administrator profile，包括姓名、邮箱、界面语言和密码。

**Original:** Before going over individual features, we recommend the following steps to set up and configure your Strapi admin panel correctly. Once you complete the setup, you can access the admin panel through the provided URL.

**中文译文:** 在逐项了解各项功能之前，建议先按照下面的步骤正确设置并配置 Strapi admin panel。完成设置后，即可通过对应 URL 访问 admin panel。

## Accessing the admin panel

**Original:** The admin panel is the back office of your Strapi application. From the admin panel, you will be able to manage content-types, and write their actual content. It is also from the admin panel that you will manage users, both administrators and end users of your Strapi application.

**中文译文:** Admin panel 是 Strapi application 的后台管理界面。你可以在这里管理 content-types 并录入实际内容，也可以管理 Strapi application 中的 administrators 与 end users。

**Original:** In order to access the admin panel, your Strapi application must be launched, and you must be aware of the URL to its admin panel (e.g. `api.example.com/admin`).

**中文译文:** 要访问 admin panel，Strapi application 必须已经启动，并且你需要知道其 admin panel URL，例如 `api.example.com/admin`。

**Original:** To access the admin panel:
1. Go to the URL of your Strapi application's admin panel.
2. Enter your credentials to log in.
3. Click on the **Login** button. You should be redirected to the homepage of the admin panel.

**中文译文:** 访问 admin panel：
1. 打开 Strapi application 的 admin panel URL；
2. 输入 credentials；
3. 点击 **Login**。登录成功后会跳转到 admin panel 首页。

### Using SSO for authentication

**Original:** If your Strapi application was configured to allow authentication through SSO, you can access the admin panel using a specific provider instead of logging in with a regular Strapi administrator account.

**中文译文:** 如果 Strapi application 已配置 [SSO](/cms/features/sso) authentication，可以通过指定 provider 访问 admin panel，而无需使用普通 Strapi administrator account 登录。

**Original:** To do so, in the login page of your Strapi application, click on a chosen provider. If you cannot see your provider, click the menu button to access the full list of all available providers. You will be redirected to your provider's own login page where you will be able to authenticate.

**中文译文:** 在 Strapi application 登录页点击所需 provider。如果没有看到目标 provider，可点击菜单按钮查看全部可用 providers。随后页面会跳转到该 provider 自己的登录页面完成 authentication。

## Setting up your administrator profile

**Original:** If you are a new administrator, we recommend making sure your profile is all set, before diving into your Strapi application. From your administrator profile, you are able to modify your user information, such as name, username, email or password. You can also choose the language of the interface for your Strapi application.

**中文译文:** 如果你是新的 administrator，建议在开始使用 Strapi application 前先完善 profile。Administrator profile 中可以修改姓名、username、email、password 等用户信息，也可以选择 Strapi application 的界面语言。

**Original:** To modify your user information:
1. Click on your account name or initials in the bottom left hand corner of the main navigation of your Strapi application.
2. In the drop-down menu, click on **Profile**.
3. Modify the information of your choice:

| Profile & Experience | Instructions |
|---|---|
| First name | Write your first name in the textbox. |
| Last name | Write your last name in the textbox. |
| Email | Write your complete email address in the textbox. |
| Username | (optional) Write a username in the textbox. |
| Interface language | Among the drop-down list, choose a language for your Strapi application interface. |
| Interface mode | Among the drop-down list, choose a mode for your Strapi application interface: either "Light mode" or "Dark mode". Note that by default, the chosen mode for a Strapi application is based on the browser's mode. |

4. Click on the **Save** button.

**中文译文:** 修改用户信息：
1. 点击 Strapi application 主导航左下角的账户名称或 initials；
2. 在下拉菜单中点击 **Profile**；
3. 根据需要修改：

| Profile & Experience | 说明 |
|---|---|
| First name | 输入名字。 |
| Last name | 输入姓氏。 |
| Email | 输入完整 email address。 |
| Username | （可选）输入 username。 |
| Interface language | 从下拉列表选择 Strapi application 的界面语言。 |
| Interface mode | 从下拉列表选择 “Light mode” 或 “Dark mode”。默认情况下，Strapi application 会跟随 browser mode。 |

4. 点击 **Save**。

### Changing your password

**Original:** To change the password of your account:
1. Go to your administrator profile.
2. Fill in the password-related options:

| Password modification | Instructions |
|---|---|
| Current password | Write your current password in the textbox. You can click the eye icon for the password to be shown. |
| Password | Write the new password in the textbox. You can click the eye icon for the password to be shown. |
| Password confirmation | Write the same new password in the textbox. You can click the eye icon for the password to be shown. |

3. Click on the **Save** button.

**中文译文:** 修改账户 password：
1. 打开 administrator profile；
2. 填写 password 相关选项：

| Password modification | 说明 |
|---|---|
| Current password | 输入当前 password；可点击 eye 图标显示内容。 |
| Password | 输入新的 password；可点击 eye 图标显示内容。 |
| Password confirmation | 再次输入相同的新 password；可点击 eye 图标显示内容。 |

3. 点击 **Save**。

**Original:** Congratulations on being a new Strapi user! You're now ready to discover all the features and options that Strapi has to offer!

**中文译文:** 恭喜你成为新的 Strapi 用户！现在可以开始探索 Strapi 提供的各项功能与配置选项了。
