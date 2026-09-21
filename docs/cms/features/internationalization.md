# 📖 对照翻译：Internationalization (i18n)

> Source: `docusaurus/docs/cms/features/internationalization.md`  
> Upstream SHA: `a578d0df8d478eecc8584c2697bdeddc90a948b5`

**Original:** Internationalization manages content in multiple locales directly from the admin panel. This documentation explains how to add locales, translate entries, and control locale-specific permissions.

**中文译文:** Internationalization（i18n）允许直接在 admin panel 中管理多个 locales 的内容。本页介绍如何添加 locale、翻译 entries，以及使用 locale 相关能力。

**Original:** The Internationalization feature allows you to manage content in different languages, called "locales".

**中文译文:** Internationalization 功能允许使用不同语言管理内容，这些语言在 Strapi 中称为 “locales”。

**Original:** Plan: Free feature. Role & permission: None. Activation: available but disabled by default. Environment: Development & Production.

**中文译文:** 功能属性：Free feature；没有额外 role/permission 要求；功能可用但默认关闭；Development 与 Production environment 均支持。

## Configuration

**Original:** Before use in Content Manager, Internationalization must be configured in Settings and enabled for content types in Content-type Builder.

**中文译文:** 在 Content Manager 中使用前，需要先在 *Settings* 中配置 Internationalization，并在 Content-Type Builder 中为相应 content types 启用该功能。

### Content-type Builder

**Original:** Path: Content-type Builder.

**中文译文:** 配置路径：*Content-Type Builder*。

**Original:** Internationalization can be configured per content type and/or field.
1. Edit or create a content type/field.
2. Open Advanced settings.
3. Enable Internationalization at content-type level and Enable localization for this field at field level.

**中文译文:** Internationalization 可以按 content type 和 field 分别配置：
1. 编辑已有 content type / field，或创建新的；
2. 打开 **Advanced settings**；
3. 在 content-type level 勾选 **Internationalization**，在 field level 勾选 **Enable localization for this field**。

### Settings

**Original:** Path: Settings > Global Settings > Internationalization.

**中文译文:** 配置路径：*Settings > Global Settings > Internationalization*。

**Original:** The Internationalization interface lists all locales available for the application. By default only English is configured and set as default.

**中文译文:** *Internationalization* 界面会列出 application 当前可用的全部 locales。默认只有 English locale，并且它是 default locale。

**Original:** Each locale shows ISO code, optional display name, and whether it is the default. Administrators can edit or delete locales.

**中文译文:** 每个 locale 会显示 ISO code、可选 display name，以及是否为 default locale。Administrator 可以编辑或删除 locale。

#### Adding a new locale

**Original:** Administrators can add as many locales as they want, but only one can be the default for the application. Custom locales cannot be created; locales must come from Strapi's 500+ predefined list.

**中文译文:** Administrator 可以添加任意数量的 locales，但整个 Strapi application 只能有一个 default locale。不能创建完全自定义的 locale；必须从 Strapi 提供的 500+ 预定义 locale 列表中选择。

**Original:** 1. Click **Add new locale**.
2. Choose a locale from the Locales dropdown.
3. Optionally enter a Locale display name.
4. Optionally enable Set as default locale.
5. Click **Save**.

**中文译文:** 1. 点击 **Add new locale**；
2. 从 *Locales* 下拉列表选择 locale；
3. （可选）填写 *Locale display name*；
4. （可选）在 Advanced settings 中启用 *Set as default locale*；
5. 点击 **Save**。

#### Enabling AI-powered internationalization

**Original:** AI-Powered Internationalization automatically translates all locales when content in the default locale is updated.

**中文译文:** AI-Powered Internationalization 会在 default locale 内容更新时，自动为项目中的其他 locales 生成翻译。

**Original:** It is disabled by default. Enable it at Settings > Global Settings > Internationalization by setting AI Translations to Enabled.

**中文译文:** 该功能默认关闭。进入 *Settings > Global Settings > Internationalization*，将 **AI Translations** 设置为 **Enabled** 即可开启。

### Code-based configuration

**Original:** `STRAPI_PLUGIN_I18N_INIT_LOCALE_CODE` can set the default locale for the environment. The value must be an ISO country code from Strapi's predefined locale list.

**中文译文:** 可以通过 `STRAPI_PLUGIN_I18N_INIT_LOCALE_CODE` environment variable 设置 environment 的 default locale。值必须是 Strapi 预定义 locale 列表中的 ISO code。

## Usage

**Original:** Path: Content Manager, edit view of the content type.

**中文译文:** 使用路径：*Content Manager*，content type 的 edit view。

**Original:** When Internationalization is enabled, a locale dropdown appears at the top-right of the edit view and allows switching locales.

**中文译文:** Content-type 启用 Internationalization 后，edit view 右上角会出现 locale 下拉列表，用于切换 locale。

**Original:** The selected locale persists when navigating between content types.

**中文译文:** 所选 locale 会在切换 content types 时保持。例如在某个 content-type 中选择 Spanish，切换到另一个 content type 后仍会保持 Spanish，即使后者没有启用 Internationalization。

**Original:** Dynamic zones and components can differ across locales. Dynamic zones may have different structures, and repeatable components may have different entries or order.

**中文译文:** Dynamic zones 和 components 可以在不同 locales 中拥有不同内容结构。Dynamic zones 可以采用不同结构；repeatable components 也可以包含不同 entries 或不同排序。

**Original:** Content can only be managed one locale at a time. Publishing affects only the locale currently being edited.

**中文译文:** 同一时间只能管理一个 locale 的内容。点击 **Publish** 时，只会发布当前正在编辑的 locale。

**Original:** To translate content:
1. Open the locale dropdown.
2. Choose the target locale.
3. Fill the content-type fields in that locale.

**中文译文:** 翻译内容：
1. 点击 edit view 右上角的 locale 下拉列表；
2. 选择目标 locale；
3. 填写该 locale 下的 content-type fields。

**Original:** Fill in from another locale copies values from another locale, including relations. It is hidden when AI-powered internationalization is enabled. For localizable relations, Strapi uses the corresponding target-locale entry if it exists; non-localizable relations reuse the exact same entry.

**中文译文:** **Fill in from another locale** 可以把另一个 locale 的 fields（包括 relations）复制到当前 locale。启用 AI-powered internationalization 后，该按钮不会显示。对于 localizable relations，如果目标 locale 中存在对应 entry，Strapi 会自动关联它；不存在时不会填充。Non-localizable relations 则直接使用完全相同的 entry。

### AI-powered internationalization

**Original:** When enabled, updating and saving content in the default locale automatically translates all other locales. The default locale is the single source of truth.

**中文译文:** 启用后，只要在 default locale 中编辑并 **Save**，其他 locales 会自动翻译；default locale 是唯一 source of truth。

**Original:** Editing non-default locales does not trigger automatic translations. Saving the default locale can overwrite manual edits made in other locales. The feature consumes Strapi AI credits.

**中文译文:** 编辑非 default locale 不会触发自动翻译；重新保存 default locale 时，其他 locales 中的手动修改可能被覆盖。该功能会消耗 Strapi AI credits。

### Usage with APIs

**Original:** Localized content can be requested, created, updated, and deleted through REST API and GraphQL API using locale parameters. Document Service API can also interact with localized content on the back end.

**中文译文:** Localized content 可以通过 REST API 与 GraphQL API 的 locale parameter 进行查询、创建、更新和删除；在 Strapi back-end 中，也可以通过 Document Service API 操作 localized content。

**Original:** REST API: use the locale parameter. GraphQL API: use locale. Document Service API: use locale.

**中文译文:** 相关文档：[REST API locale](/cms/api/rest/locale)、[GraphQL API locale](/cms/api/graphql#locale)、[Document Service API locale](/cms/api/document-service/locale)。
