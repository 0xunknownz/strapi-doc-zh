# 📖 对照翻译：Admin Panel API — Navigation & settings

> Source: `docusaurus/docs/cms/plugins-development/admin-navigation-settings.md`  
> Upstream SHA: `f58f2ba1cf734117b94ecc1d6c610f1ca8747a17`

**Original:** Use `addMenuLink` for sidebar navigation and `addSettingsLink` to create or extend settings sections.

**中文译文:** Plugin 可以通过 Admin Panel API：
- 使用 `addMenuLink()` 向左侧 main navigation 增加入口；
- 使用 `addSettingsLink()` 创建新的 settings section，或向已有 section 增加页面。

## Navigation sidebar

### `addMenuLink()`

| Parameter | Required | 中文说明 |
|---|---:|---|
| `to` | Yes | 相对 admin root 的 path |
| `icon` | Yes | React icon component |
| `intlLabel` | Yes | `id` + `defaultMessage` |
| `permissions` | Yes | 控制 link visibility 的 permission array |
| `Component` | No | Dynamic import page component |
| `position` | No | Menu 排序，数值越小越靠前 |
| `licenseOnly` | No | 显示付费 feature ⚡ 标记 |
| `target` | No | Anchor target，例如 `_blank` |
| `notificationsCount` | No | Menu badge count |
| `exact` | No | Active route 是否精确匹配 |

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
  permissions: [],
  position: 3,
  licenseOnly: false,
});
```

**Original:** The page module used by `Component` should default-export the component.

**中文译文:** `Component: () => import(path)` 期望目标 module 使用 **default export**。旧版支持 async callback 返回 named export 的写法已经 deprecated，并会产生 runtime warning。

**Original:** Link permissions only control visibility; they do not secure the page.

**中文译文:** **`permissions` 只控制 navigation link 是否可见，不等于 route authorization。** 用户知道 URL 时仍可能直接访问页面。真正安全控制还要在 page component 检查 permissions，并在 server 注册 RBAC actions。

## Settings — create a section

**Original:** Use `addSettingsLink(sectionObject, links)`.

```js
app.addSettingsLink(
  {
    id: 'my-plugin',
    intlLabel: {
      id:
        'my-plugin.settings.section-label',
      defaultMessage:
        'My Plugin Settings',
    },
  },
  [
    {
      id: 'general',
      to: 'my-plugin/general',
      intlLabel: {
        id:
          'my-plugin.settings.general',
        defaultMessage:
          'General',
      },
      Component:
        () =>
          import(
            './pages/Settings/General'
          ),
      permissions: [],
    },
  ]
);
```

**中文译文:** 第一参数是 section definition；第二参数是 settings links array。新 section 通常在 `register()` 中创建。

## Add links to existing sections

**Original:** Use `addSettingsLink(sectionId, linkOrLinks)` in `bootstrap()`.

```js
app.addSettingsLink(
  'global',
  {
    id: 'documentation',
    to:
      'my-plugin/documentation',
    intlLabel: {
      id:
        'my-plugin.settings.documentation',
      defaultMessage:
        'Documentation',
    },
    Component:
      () =>
        import(
          './pages/Settings/Documentation'
        ),
    permissions: [],
  }
);
```

**中文译文:** Built-in section IDs：
- `global`：General application settings；
- `permissions`：Administration panel settings。

向其他 plugin 创建的 section 加 link 时建议放在 `bootstrap()`，确保 target section 已注册。

## Path conventions

| Context | `to` | Final path |
|---|---|---|
| `addMenuLink` | `/plugins/my-plugin` | `/admin/plugins/my-plugin` |
| Settings | `my-plugin/general` | `/admin/settings/my-plugin/general` |

**中文译文:** Settings link 的 `to` 不要包含 `settings/` prefix。

## Deprecated methods

**Original:** `createSettingSection()` and `addSettingsLinks()` are deprecated.

**中文译文:** 旧 API：
- `createSettingSection(section, links)`
- `addSettingsLinks(sectionId, links)`

目前仍兼容，但新代码统一使用 `addSettingsLink()`：
- 第一参数传 section object → 创建 section；
- 第一参数传 section ID string → 扩展已有 section；
- 第二参数既可以单个 link，也可以 array。
