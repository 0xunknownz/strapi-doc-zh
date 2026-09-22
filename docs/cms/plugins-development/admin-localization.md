# 📖 对照翻译：Admin Panel API — Localization

> Source: `docusaurus/docs/cms/plugins-development/admin-localization.md`  
> Upstream SHA: `50372bc745455eb70f4c4f6f55b009f965b5c653`

**Original:** Register translation files with `registerTrads`, prefix keys with your plugin ID, and use `react-intl` in components.

**中文译文:** Plugin admin UI 可以通过 `registerTrads()` 注册多语言文件；translation key 必须加 plugin ID prefix，避免与 Strapi core 或其他 plugin 冲突。React component 中使用 `react-intl` 读取 translation。

## Translation files

```text
admin/src/translations/
  ├── en.json
  ├── fr.json
  └── de.json
```

```json
{
  "plugin.name": "My Plugin",
  "plugin.description": "A custom Strapi plugin",
  "settings.title": "Settings"
}
```

## `registerTrads()`

**Original:** Strapi calls this async function during admin initialization and merges returned translations with core translations.

**中文译文:** Admin panel 初始化时，Strapi 会调用全部 plugin 的 `registerTrads()`，收集并 merge translations。

```js
import {
  prefixPluginTranslations,
} from './utils/prefixPluginTranslations';

import {
  PLUGIN_ID,
} from './pluginId';

export default {
  register(app) {
    app.registerPlugin({
      id: PLUGIN_ID,
      name: 'My Plugin',
    });
  },

  async registerTrads({
    locales,
  }) {
    return Promise.all(
      locales.map((locale) =>
        import(
          `./translations/${locale}.json`
        )
          .then(({ default: data }) => ({
            data:
              prefixPluginTranslations(
                data,
                PLUGIN_ID
              ),
            locale,
          }))
          .catch(() => ({
            data: {},
            locale,
          }))
      )
    );
  },
};
```

**中文译文:** `locales` 是当前 admin panel configured locale codes。某 locale 没有 translation file 时应返回空 object，而不是抛错导致 admin 初始化失败。

## Return value

```ts
{
  data: Record<string, string>;
  locale: string;
}
```

**中文译文:** `registerTrads()` 返回 Promise，resolved value 是上述 object array。

## Prefix translation keys

**Original:** Translation keys must be namespaced with the plugin ID.

**中文译文:** 如果原 key 为：
- `plugin.name`
- `settings.title`

Plugin ID 为 `my-plugin` 时，应转换为：
- `my-plugin.plugin.name`
- `my-plugin.settings.title`

```js
const prefixPluginTranslations =
  (trad, pluginId) => {
    if (!pluginId) {
      throw new TypeError(
        "pluginId can't be empty"
      );
    }

    return Object
      .keys(trad)
      .reduce((acc, key) => {
        acc[
          `${pluginId}.${key}`
        ] = trad[key];

        return acc;
      }, {});
  };
```

## Use in React components

```jsx
import {
  useIntl,
} from 'react-intl';

const HomePage = () => {
  const {
    formatMessage,
  } = useIntl();

  return (
    <h1>
      {formatMessage({
        id: 'my-plugin.plugin.name',
        defaultMessage:
          'My Plugin',
      })}
    </h1>
  );
};
```

**中文译文:** 始终提供 `defaultMessage`，即使 translation 缺失也能显示合理 fallback。

## Translation helper

```js
export const getTranslation =
  (id) =>
    `${PLUGIN_ID}.${id}`;
```

**中文译文:** 可用 helper 统一生成 prefixed key，避免 component 中重复手写 plugin ID。

## Translation in admin configuration

```js
app.addMenuLink({
  to: '/plugins/my-plugin',
  icon: PluginIcon,
  intlLabel: {
    id: 'my-plugin.plugin.name',
    defaultMessage:
      'My Plugin',
  },
  Component:
    () => import('./pages/App'),
});
```

## Loading order

**中文译文:** Admin translation lifecycle：
1. Core translations 先加载；
2. 各 plugin 的 `registerTrads()` 被调用并 merge；
3. Project-level `config.translations` overrides 再应用；
4. 最终通过 `react-intl` 提供给 UI。

**Original:** English is always available and acts as the fallback locale.

**中文译文:** `en` 始终可用，并作为 fallback locale。建议 plugin 至少提供 English translation。

## Best practices

**中文译文:**
- Translation key 始终加 plugin prefix；
- `formatMessage` 提供 `defaultMessage`；
- Missing locale file 返回 `{}` 而不是 throw；
- 使用层次化、可读 key 名；
- 至少支持 English；
- 使用多个 admin locales 实际测试 plugin。
