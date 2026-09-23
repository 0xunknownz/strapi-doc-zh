# 📖 对照翻译：Documentation 插件

> Source: `docusaurus/docs/cms/plugins/documentation.md`  
> Upstream commit: `d3cbe0c728c53920d40e3963c0a57cca0d68dbeb`  
> Upstream blob SHA: `45afc1e90e1c80d9a01fd44bd4c9d691550bceb4`  
> [查看固定版本英文源文件](https://github.com/strapi/documentation/blob/d3cbe0c728c53920d40e3963c0a57cca0d68dbeb/docusaurus/docs/cms/plugins/documentation.md)

> 排版说明：MDX 的链接与图标转换为 GitHub 可读形式；正文、表格和提示逐项对照，代码块保留原样。页面元数据中的描述也在下方翻译。

**Original:** By using Swagger UI, the API documentation plugin takes out most of your pain to generate your documentation.

**中文译文:** API 文档插件借助 Swagger UI，大幅简化了文档生成工作。

<a id="documentation-plugin"></a>

**Original:** Documentation plugin

**中文译文:** Documentation 插件

**Original:** The Documentation plugin auto-generates OpenAPI/Swagger docs for your API by scanning content types and routes. This documentation walks you through installation, customizing settings, and restricting access to the docs.

**中文译文:** Documentation 插件通过扫描内容类型和路由，为 API 自动生成 OpenAPI/Swagger 文档。本页介绍安装、自定义设置以及限制文档访问的方法。

**Original:** The Documentation plugin automates your API documentation creation. It basically generates a swagger file. It follows the [Open API specification version](https://swagger.io/specification/).

**中文译文:** Documentation 插件可自动创建 API 文档，本质上是生成一个 Swagger 文件。它遵循相应版本的 [OpenAPI 规范](https://swagger.io/specification/)。

**Original:** **Location** — Usable via the admin panel.<br/>Configured through both admin panel and server code, with different sets of options.

**中文译文:** **使用位置** — 可通过管理面板使用。<br/>管理面板和服务端代码均可用于配置，但两者提供的选项不同。

**Original:** **Package name** — `@strapi/plugin-documentation`

**中文译文:** **包名** — `@strapi/plugin-documentation`

**Original:** **Additional resources** — [Strapi Marketplace page](https://community.strapi.io/marketplace/strapi-plugin-documentation)

**中文译文:** **更多资源** — [Strapi Marketplace 页面](https://community.strapi.io/marketplace/strapi-plugin-documentation)

> **caution Unmaintained plugin / 注意：缺乏持续维护的插件**

**Original:** The Documentation plugin is not actively maintained and may not work with Strapi 5.

**中文译文:** Documentation 插件目前未得到积极维护，可能无法在 Strapi 5 上正常运行。

> **排版说明：交互演示。** 原文在此嵌入 Guideflow 演示（`lightId="5pvjz4zswp"`、`darkId="6kw4vdwizp"`）。GitHub Markdown 无法运行该组件，请在[上游文档页面](https://docs.strapi.io/cms/plugins/documentation)查看。

**Original:** If installed, the Documentation plugin will inspect content types and routes found on all APIs in your project and any plugin specified in the configuration. The plugin will then programmatically generate documentation to match the [OpenAPI specification](https://swagger.io/specification/). The Documentation plugin generates the [paths objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#paths-object) and [schema objects](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schema-object) and converts all Strapi types to [OpenAPI data types](https://swagger.io/docs/specification/data-models/data-types/).

**中文译文:** 安装后，Documentation 插件会检查项目中所有 API，以及配置中指定的各插件所包含的内容类型和路由。随后，它会以编程方式生成符合 [OpenAPI 规范](https://swagger.io/specification/)的文档。Documentation 插件会生成[路径对象](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#paths-object)和[模式对象](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#schema-object)，并将所有 Strapi 类型转换为 [OpenAPI 数据类型](https://swagger.io/docs/specification/data-models/data-types/)。

**Original:** The generated documentation JSON file can be found in your application at the following path: `src/extensions/documentation/documentation/<version>/full_documentation.json`

**中文译文:** 生成的文档 JSON 文件位于应用中的以下路径：`src/extensions/documentation/documentation/<version>/full_documentation.json`。

<a id="installation"></a>

## Installation / 安装

**Original:** To install the documentation plugin, run following command in your terminal:

**中文译文:** 在终端中运行以下命令，安装 Documentation 插件：

```bash
yarn add @strapi/plugin-documentation
```

```bash
npm install @strapi/plugin-documentation
```

**Original:** Once the plugin is installed, starting Strapi generates the API documentation.

**中文译文:** 插件安装完成后，启动 Strapi 即可生成 API 文档。

<a id="configuration"></a>

## Configuration / 配置

**Original:** Most configuration options for the Documentation plugin are handled via your Strapi project's code. A few settings are available in the admin panel.

**中文译文:** Documentation 插件的大多数选项需要在 Strapi 项目的代码中配置，少量设置也可通过管理面板调整。

<a id="admin-panel-settings"></a>

### Admin panel settings / 管理面板设置

**Original:** The Documentation plugin affects multiple parts of the admin panel. The following table lists all the additional options and settings that are added to a Strapi application once the plugin has been installed:

**中文译文:** Documentation 插件会影响管理面板中的多个区域。下表列出安装插件后，Strapi 应用新增的全部选项和设置：

**Original:**

| Section impacted    | Options and settings         |
|------------------|-------------------------------------------------------------|
| Documentation    | <ul>Addition of a new Documentation option in the main navigation ℹ️ which shows a panel with buttons to 👁️ open and ↻ regenerate the documentation.</ul>        |
| Settings     | <ul><li>Addition of a "Documentation plugin" setting section, which controls whether the documentation endpoint is private or not (see [restricting access](#restrict-access)).<br/> 👉 Path reminder: ⚙️ *Settings > Documentation plugin* </li><br/>  <li> Activation of role based access control for accessing, updating, deleting, and regenerating the documentation. Administrators can authorize different access levels to different types of users in the *Plugins* tab and the *Settings* tab (see [Users & Permissions documentation](/cms/features/users-permissions)).<br/>👉 Path reminder: ⚙️ *Settings > Administration Panel > Roles* </li></ul>|

**中文译文:**

| 受影响的区域 | 选项与设置 |
|---|---|
| Documentation | 主导航中新增 Documentation 入口 ℹ️，打开后会显示操作面板，其中包含用于打开 👁️ 和重新生成 ↻ 文档的按钮。 |
| Settings | 新增“Documentation plugin”设置区域，用于控制文档端点是否需要限制访问（参见[限制访问](#restrict-access)）。<br/>👉 访问路径：⚙️ *Settings > Documentation plugin*。<br/><br/>启用基于角色的访问控制，分别管理访问、更新、删除和重新生成文档的权限。管理员可在 *Plugins* 和 *Settings* 选项卡中，为不同类型的用户授予不同的访问级别（参见 [Users & Permissions 文档](/cms/features/users-permissions)）。<br/>👉 访问路径：⚙️ *Settings > Administration Panel > Roles*。 |

<a id="restrict-access"></a>

#### Restricting access to your API documentation / 限制 API 文档的访问

**Original:** By default, your API documentation will be accessible by anyone.

**中文译文:** 默认情况下，任何人都可以访问 API 文档。

**Original:** To restrict API documentation access, enable the **Restricted Access** option from the admin panel:

**中文译文:** 要限制 API 文档的访问，请在管理面板中启用 **Restricted Access**：

**Original:**

1. Navigate to ⚙️ *Settings* in the main navigation of the admin panel.
2. Choose **Documentation**.
3. Toggle **Restricted Access** to `ON`.
4. Define a password in the `password` input.
5. Save the settings.

**中文译文:**

1. 在管理面板的主导航中，进入 ⚙️ *Settings*。
2. 选择 **Documentation**。
3. 将 **Restricted Access** 切换为 `ON`。
4. 在 `password` 输入框中设置密码。
5. 保存设置。

<a id="code-based-configuration"></a>

### Code-based configuration / 通过代码配置

**Original:** To configure the Documentation plugin, create a `settings.json` file in the `src/extensions/documentation/config` folder. In this file, you can specify all your environment variables, licenses, external documentation links, and all the entries listed in the [specification](https://swagger.io/specification/).

**中文译文:** 要配置 Documentation 插件，请在 `src/extensions/documentation/config` 文件夹中创建 `settings.json` 文件。你可以在其中指定环境变量、许可证、外部文档链接，以及[规范](https://swagger.io/specification/)中列出的所有条目。

**Original:** The following is an example configuration:

**中文译文:** 以下是一个配置示例：

```json title="src/extensions/documentation/config/settings.json"
{
  "openapi": "3.0.0",
  "info": {
    "version": "1.0.0",
    "title": "DOCUMENTATION",
    "description": "",
    "termsOfService": "YOUR_TERMS_OF_SERVICE_URL",
    "contact": {
      "name": "TEAM",
      "email": "contact-email@something.io",
      "url": "mywebsite.io"
    },
    "license": {
      "name": "Apache 2.0",
      "url": "https://www.apache.org/licenses/LICENSE-2.0.html"
    }
  },
  "x-strapi-config": {
    "plugins": ["upload", "users-permissions"],
    "path": "/documentation"
  },
  "servers": [
    {
      "url": "http://localhost:1337/api",
      "description": "Development server"
    }
  ],
  "externalDocs": {
    "description": "Find out more",
    "url": "https://docs.strapi.io/developer-docs/latest/getting-started/introduction.html"
  },
  "security": [
    {
      "bearerAuth": []
    }
  ]
}
```

> **tip / 提示**

**Original:** If you need to add a custom key, prefix it by `x-` (e.g., `x-strapi-something`).

**中文译文:** 添加自定义键时，请以 `x-` 为前缀，例如 `x-strapi-something`。

<a id="create-a-new-version-of-the-documentation"></a>

#### Creating a new version of the documentation / 创建新版本的文档

**Original:** To create a new version, change the `info.version` key in the `settings.json` file:

**中文译文:** 要创建新版本，请修改 `settings.json` 文件中的 `info.version`：

```json title="src/extensions/documentation/config/settings.json"
{
  "info": {
    "version": "2.0.0"
  }
}
```

**Original:** This will automatically create a new version.

**中文译文:** 这样就会自动创建一个新版本。

<a id="define-which-plugins"></a>

#### Defining which plugins need documentation generated / 指定需要生成文档的插件

**Original:** If you want plugins to be included in documentation generation, they should be included in the `plugins` array in the `x-strapi-config` object. By default, the array is initialized with `["upload", "users-permissions"]`:

**中文译文:** 要为插件生成文档，请将插件名称加入 `x-strapi-config` 对象的 `plugins` 数组中。该数组默认初始化为 `["upload", "users-permissions"]`：

```json title="src/extensions/documentation/config/settings.json"
{
  "x-strapi-config": {
    "plugins": ["upload", "users-permissions"]
  }
}
```

**Original:** To add more plugins, such as your custom plugins, add their name to the array.

**中文译文:** 要加入更多插件，例如自定义插件，只需将其名称添加到数组中。

**Original:** If you do not want plugins to be included in documentation generation, provide an empty array (i.e., `plugins: []`).

**中文译文:** 不需要为任何插件生成文档时，请提供空数组，即 `plugins: []`。

<a id="overriding-the-generated-documentation"></a>

#### Overriding the generated documentation / 覆盖生成的文档

**Original:** The Documentation plugins comes with 3 methods to override the generated documentation: [`excludeFromGeneration`](#excluding-from-generation), [`registerOverride`](#register-override), and [`mutateDocumentation`](#mutate-documentation).

**中文译文:** Documentation 插件提供 3 种覆盖生成文档的方法：[`excludeFromGeneration`](#excluding-from-generation)、[`registerOverride`](#register-override) 和 [`mutateDocumentation`](#mutate-documentation)。

<a id="excluding-from-generation"></a>

##### excludeFromGeneration() / `excludeFromGeneration()`

**Original:** To exclude certain APIs or plugins from being generated, use the `excludeFromGeneration` found on the documentation plugin’s `override` service in your application or plugin's [`register` lifecycle](/cms/plugins-development/admin-panel-api#register).

**中文译文:** 要排除某些 API 或插件，不为其生成文档，请在应用或插件的 [`register` 生命周期](/cms/plugins-development/admin-panel-api#register)中，调用 Documentation 插件 `override` 服务上的 `excludeFromGeneration` 方法。

> **note / 说明**

**Original:** `excludeFromGeneration` gives more fine-grained control over what is generated.

**中文译文:** `excludeFromGeneration` 可以更细致地控制文档生成范围。

**Original:** For example, pluginA might create several new APIs while pluginB may only want to generate documentation for some of those APIs. In that case, pluginB could still benefit from the generated documentation it does need by excluding only what it does not need.

**中文译文:** 例如，pluginA 可能创建多个新 API，而 pluginB 只需要为其中一部分生成文档。这时，pluginB 只需排除不需要的 API，仍可保留对其余 API 自动生成文档的能力。

---

**Original:**

| Parameter | Type                       | Description                                              |
| --------- | -------------------------- | -------------------------------------------------------- |
| `api`       | String or Array of Strings | The name of the API/plugin, or list of names, to exclude |

**中文译文:**

| 参数 | 类型 | 说明 |
|---|---|---|
| `api` | 字符串或字符串数组 | 要排除的 API/插件名称，或名称列表。 |

```js title="Application or plugin register lifecycle"

module.exports = {
  register({ strapi }) {
    strapi
      .plugin("documentation")
      .service("override")
      .excludeFromGeneration("restaurant");
    // or several
    strapi
      .plugin("documentation")
      .service("override")
      .excludeFromGeneration(["address", "upload"]);
  }
}
```

<a id="register-override"></a>

##### registerOverride() / `registerOverride()`

**Original:** If the Documentation plugin fails to generate what you expect, it is possible to replace what has been generated.

**中文译文:** 如果 Documentation 插件生成的内容不符合预期，可以将其替换。

**Original:** The Documentation plugin exposes an API that allows you to replace what was generated for the following OpenAPI root level keys: `paths`, `tags`, `components` .

**中文译文:** Documentation 插件提供的 API 支持替换生成文档中以下 OpenAPI 顶层键的内容：`paths`、`tags` 和 `components`。

**Original:** To provide an override, use the `registerOverride` function found on the Documentation plugin’s `override` service in your application or plugin's [`register` lifecycle](/cms/plugins-development/admin-panel-api#register).

**中文译文:** 要提供覆盖内容，请在应用或插件的 [`register` 生命周期](/cms/plugins-development/admin-panel-api#register)中，调用 Documentation 插件 `override` 服务上的 `registerOverride` 函数。

**Original:**

| Parameter                     | Type                      | Description                                                                                                   |
| ----------------------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `override`                     | Object                    | OpenAPI object including any of the following keys paths, tags, components. Accepts JavaScript, JSON, or yaml |
| `options`                      | Object                    | Accepts `pluginOrigin` and `excludeFromGeneration`                                                               |
| `options.pluginOrigin`          | String                    | The plugin that is registering the override                                                                   |
| `options.excludeFromGeneration` | String or Array of String | The name of the API/plugin, or list of names, to exclude                                                      |

**中文译文:**

| 参数 | 类型 | 说明 |
|---|---|---|
| `override` | 对象 | OpenAPI 对象，可包含 `paths`、`tags`、`components` 中的任意键。接受 JavaScript、JSON 或 YAML。 |
| `options` | 对象 | 接受 `pluginOrigin` 和 `excludeFromGeneration`。 |
| `options.pluginOrigin` | 字符串 | 注册该覆盖内容的插件名称。 |
| `options.excludeFromGeneration` | 字符串或字符串数组 | 要排除的 API/插件名称，或名称列表。 |

> **caution / 注意**

**Original:** Plugin developers providing an override should always specify the `pluginOrigin` options key. Otherwise the override will run regardless of the user’s configuration.

**中文译文:** 插件开发者提供覆盖内容时，必须指定 `pluginOrigin` 选项。否则，无论用户如何配置，覆盖内容都会生效。

**Original:** The Documentation plugin will use the registered overrides to replace the value of common keys on the generated documentation with what the override provides. If no common keys are found, the plugin will add new keys to the generated documentation.

**中文译文:** Documentation 插件会使用已注册的覆盖内容，替换生成文档中同名键的值。如果没有找到同名键，则会将新键添加到生成的文档中。

**Original:** If the override completely replaces what the documentation generates, you can specify that generation is no longer necessary by providing the names of the APIs or plugins to exclude in the options key array `excludeFromGeneration`.

**中文译文:** 如果覆盖内容已经完全替代自动生成的结果，可以在选项数组 `excludeFromGeneration` 中列出相应的 API 或插件名称，声明无需再为它们自动生成文档。

**Original:** If the override should only be applied to a specific version, the override must include a value for `info.version`. Otherwise, the override will run on all documentation versions.

**中文译文:** 如果覆盖内容只应应用于某个版本，就必须在其中指定 `info.version`。否则，覆盖内容会应用于所有文档版本。

```js title="Application or plugin register lifecycle"

module.exports = {
  register({ strapi }) {
    if (strapi.plugin('documentation')) {
      const override = {
        // Only run this override for version 1.0.0
        info: { version: '1.0.0' },
        paths: {
          '/answer-to-everything': {
            get: {
              responses: { 200: { description: "*" }}
            }
          }
        }
      }

      strapi
        .plugin('documentation')
        .service('override')
        .registerOverride(override, {
          // Specify the origin in case the user does not want this plugin documented
          pluginOrigin: 'upload',
          // The override provides everything don't generate anything
          excludeFromGeneration: ['upload'],
        });
    }
  },
}
```

**Original:** The overrides system is provided to try and simplify amending the generated documentation. It is the only way a plugin can add or modify the generated documentation.

**中文译文:** 覆盖机制旨在简化对生成文档的修改。对于插件而言，这是新增或修改生成文档的唯一方式。

<a id="mutate-documentation"></a>

##### mutateDocumentation() / `mutateDocumentation()`

**Original:** The Documentation plugin’s configuration also accepts a `mutateDocumentation` function on `info['x-strapi-config']`. This function receives a draft state of the generated documentation that be can be mutated. It should only be applied from an application and has the final say in the OpenAPI schema.

**中文译文:** Documentation 插件的配置还支持在 `info['x-strapi-config']` 上定义 `mutateDocumentation` 函数。该函数接收已生成文档的可变草稿，允许直接修改其内容。它只能由应用使用，并对最终的 OpenAPI 模式拥有最后修改权。

**Original:**

| Parameter                   | Type   | Description                                                            |
| --------------------------- | ------ | ---------------------------------------------------------------------- |
| `generatedDocumentationDraft` | Object | The generated documentation with applied overrides as a mutable object |

**中文译文:**

| 参数 | 类型 | 说明 |
|---|---|---|
| `generatedDocumentationDraft` | 对象 | 已应用覆盖内容的生成文档，以可修改的对象形式提供。 |

```js title="config/plugins.js"

module.exports = {
  documentation: {
    config: {
      "x-strapi-config": {
        mutateDocumentation: (generatedDocumentationDraft) => {
          generatedDocumentationDraft.paths[
            "/answer-to-everything" // must be an existing path
          ].get.responses["200"].description = "*";
        },
      },
    },
  },
};
```

<a id="usage"></a>

## Usage / 使用

**Original:** The Documentation plugin visualizes your API using [Swagger UI](https://swagger.io/tools/swagger-ui/). To access the UI, select ℹ️ in the main navigation of the admin panel. Then click **Open documentation** to open the Swagger UI. Using the Swagger UI you can view all of the endpoints available on your API and trigger API calls.

**中文译文:** Documentation 插件使用 [Swagger UI](https://swagger.io/tools/swagger-ui/) 将 API 可视化。要打开该界面，请先选择管理面板主导航中的 ℹ️ 入口，再点击 **Open documentation**。通过 Swagger UI，可以查看 API 的所有可用端点，并直接发起 API 调用。

> **tip / 提示**

**Original:** Once the plugin is installed, the plugin user interface can be accessed at the following URL:
`<server-url>:<server-port>/documentation/<documentation-version>`
(e.g., [`localhost:1337/documentation/v1.0.0`](http://localhost:1337/documentation/v1.0.0)).

**中文译文:** 插件安装完成后，可以通过以下 URL 访问其界面：
`<server-url>:<server-port>/documentation/<documentation-version>`
例如，[`localhost:1337/documentation/v1.0.0`](http://localhost:1337/documentation/v1.0.0)。

<a id="regenerate-documentation"></a>

### Regenerating documentation / 重新生成文档

**Original:** There are 2 ways to update the documentation after making changes to your API:

**中文译文:** 修改 API 后，可以通过以下 2 种方式更新文档：

**Original:**

- restart your application to regenerate the version of the documentation specified in the Documentation plugin's configuration,
- or go to the Documentation plugin page and click the **regenerate** button for the documentation version you want to regenerate.

**中文译文:**

- 重启应用，重新生成 Documentation 插件配置中指定版本的文档。
- 或进入 Documentation 插件页面，点击目标文档版本对应的 **regenerate** 按钮。

<a id="authenticating-requests"></a>

### Authenticating requests / 为请求提供认证信息

**Original:** Strapi is secured by default, which means that most of your endpoints require the user to be authorized. If the CRUD action has not been set to Public in the [Users & Permissions feature](/cms/features/users-permissions#roles) then you must provide your JSON web token (JWT). To do this, while viewing the API Documentation, click the **Authorize** button and paste your JWT in the _bearerAuth_ _value_ field.

**中文译文:** Strapi 默认启用安全保护，因此大多数端点都要求用户具备相应权限。如果尚未在 [Users & Permissions 功能](/cms/features/users-permissions#roles)中将相应 CRUD 操作开放给 Public 角色，就必须提供 JSON Web Token（JWT）。操作方法是：打开 API 文档，点击 **Authorize**，然后将 JWT 粘贴到 _bearerAuth_ 的 _value_ 字段中。

> **译者注：原文配置位置存在不一致。** `mutateDocumentation()` 的说明文字写作 `info['x-strapi-config']`，但原文代码将其放在 `documentation.config["x-strapi-config"]` 下。本译文保留这一区别，没有擅自改写英文或示例。该插件的 Strapi 5 兼容性警告也按原文保留。
