# 📖 对照翻译：Admin Panel API — Injection zones

> Source: `docusaurus/docs/cms/plugins-development/admin-injection-zones.md`  
> Upstream SHA: `a663b09967cf2b2a145936a99e4dee9cdcf3f34c`

**Original:** Injection zones are predefined or plugin-defined admin UI areas where React components can be injected.

**中文译文:** Injection zone 是 admin UI 中预留的 component extension point。Plugin 可以：
- 向 Strapi / Content Manager 已有 zone 注入 React component；
- 在自己的 plugin UI 中声明 custom zones，允许其他 plugins 扩展。

**Original:** Zones are declared in `register()`; components are injected in `bootstrap()`.

**中文译文:** 生命周期规则：
- Zone **声明**：`register()`
- Component **注入**：`bootstrap()`

## Predefined Content Manager zones

| View | Zone | 中文说明 |
|---|---|---|
| List | `listView.actions` | Filters 与 cog icon 之间 |
| List | `listView.publishModalAdditionalInfos` | Publish confirmation modal 信息区 |
| List | `listView.unpublishModalAdditionalInfos` | Unpublish modal 信息区 |
| List | `listView.deleteModalAdditionalInfos` | Delete modal 信息区 |
| Edit | `editView.right-links` | Configure view / Edit controls 附近 |
| Edit | `editView.informations` | Informations box，属于 internal zone |
| Preview | `preview.actions` | Preview action area |

**Original:** `editView.informations` is internal; `editView.right-links` is the stable recommended Edit View extension point.

**中文译文:** Third-party plugin 应优先使用 `editView.right-links`。`editView.informations` 虽然存在，但属于 internal zone，未来 UI 版本更容易变化。

## Inject into Content Manager

```jsx
export default {
  bootstrap(app) {
    app
      .getPlugin(
        'content-manager'
      )
      .injectComponent(
        'editView',
        'right-links',
        {
          name:
            'my-plugin-custom-button',
          Component:
            MyCustomButton,
        }
      );

    app
      .getPlugin(
        'content-manager'
      )
      .injectComponent(
        'listView',
        'actions',
        {
          name:
            'my-plugin-list-action',
          Component:
            () =>
              <button>
                Custom List Action
              </button>,
        }
      );
  },
};
```

## Custom injection zones

**Original:** Declare zones in `registerPlugin({ injectionZones })`.

```js
app.registerPlugin({
  id: 'dashboard',
  name: 'Dashboard',

  injectionZones: {
    homePage: {
      top: [],
      middle: [],
      bottom: [],
    },

    sidebar: {
      before: [],
      after: [],
    },
  },
});
```

## Rendering custom zones in Strapi 5

**Original:** The old `InjectionZone` component from `@strapi/helper-plugin` no longer exists.

**中文译文:** Strapi 5 已移除旧 `@strapi/helper-plugin` 的 `InjectionZone` component。Custom plugin 需要通过 `useStrapiApp` 获取 target plugin 的 injected components 并自行 render。

```jsx
import {
  useStrapiApp,
} from '@strapi/strapi/admin';

export const CustomInjectionZone =
  ({ area, ...props }) => {
    const getPlugin =
      useStrapiApp(
        'CustomInjectionZone',
        (state) =>
          state.getPlugin
      );

    const [
      pluginName,
      view,
      zone,
    ] =
      area.split('.');

    const plugin =
      getPlugin(pluginName);

    const components =
      plugin
        ?.getInjectedComponents(
          view,
          zone
        );

    if (
      !components?.length
    ) {
      return null;
    }

    return components.map(
      ({
        name,
        Component,
      }) => (
        <Component
          key={name}
          {...props}
        />
      )
    );
  };
```

## Inject into another plugin's custom zone

```js
bootstrap(app) {
  const dashboard =
    app.getPlugin(
      'dashboard'
    );

  if (dashboard) {
    dashboard
      .injectComponent(
        'homePage',
        'top',
        {
          name:
            'widget-plugin-statistics',
          Component:
            Widget,
        }
      );
  }
}
```

**中文译文:** 注入前先检查 target plugin 是否存在，避免 plugin 未安装时 admin bootstrap 崩溃。

## Content Manager context

**Original:** Injected components can read Edit View state through `unstable_useContentManagerContext`.

**中文译文:** Content Manager injection component 可以使用：

`unstable_useContentManagerContext`

读取：
- `slug`
- `model`
- `id`
- `collectionType`
- `isCreatingEntry`
- `isSingleType`
- `hasDraftAndPublish`
- `contentType`
- `components`
- `layout`
- `form`

并通过 `form.onChange` 修改 form state。

**Original:** The `unstable_` prefix means the API may change.

**中文译文:** `unstable_` 明确表示该 API 可能在后续版本改变。它替代了 Strapi 4 的 deprecated `useCMEditViewDataManager`。

## Best practices

**中文译文:**
- Zone name 使用清晰语义，例如 `top`、`before`；
- 注入第三方 plugin 前检查 `getPlugin()` 返回值；
- Component name 保持全局唯一；
- 对可能不存在的 zone graceful fallback；
- Plugin 对外暴露 custom injection zones 时应写清 view/zone contract。
