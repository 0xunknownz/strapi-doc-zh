# 📖 对照翻译：Plugins configuration

> Source: `docusaurus/docs/cms/configurations/plugins.md`  
> Upstream SHA: `8d5613fa4e9370efa0d24f461906bace1a2a54b2`

**Original:** `/config/plugins` enables or disables plugins and overrides their settings, with support for local plugin development.

**中文译文:** `/config/plugins.js|ts` 用于启用 / 禁用 plugin、覆盖 plugin default configuration，以及声明 local plugin 的 source path。

| Parameter | Type | 中文说明 |
|---|---|---|
| `enabled` | Boolean | 显式启用 / 禁用已安装 plugin |
| `config` | Object | 可选；覆盖 plugin server 默认配置 |
| `resolve` | String | 可选；local plugin 必需，指向 plugin folder |

**Original:** Some core features are still configured through `config/plugins` for historical reasons.

**中文译文:** Strapi 5 中部分能力虽然已不再被视为普通 plugin，但为了兼容配置结构仍从 `config/plugins` 读取，例如：
- Upload / Media Library；
- Users & Permissions；
- GraphQL plugin。

Email / Upload provider config 也定义在 `config/plugins`。

## Example

**Original code (kept unchanged):**

```js title="./config/plugins.js"
module.exports = ({ env }) => ({
  i18n: true,

  myplugin: {
    enabled: true,
    resolve: './src/plugins/my-local-plugin',
    config: {
      // user plugin config goes here
    },
  },

  'my-other-plugin': {
    enabled: false,
  },
});
```

**中文译文:** 示例展示：
- 使用 shorthand `i18n: true` 启用无需配置的 plugin；
- 通过 `resolve` 加载 local plugin；
- 使用 `config` 传入用户配置；
- 将已安装 plugin 显式设为 disabled。

**Original:** A plugin requiring no configuration can use shorthand `'plugin-name': true`.

**中文译文:** 如果无需传额外配置，可以直接使用：

`'plugin-name': true`
