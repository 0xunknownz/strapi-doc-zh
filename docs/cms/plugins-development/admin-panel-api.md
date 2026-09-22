# 📖 对照翻译：Admin Panel API for plugins — Overview

> Source: `docusaurus/docs/cms/plugins-development/admin-panel-api.md`  
> Upstream SHA: `87d41015f7a4425a9d631663210d96b8bf059c68`

**Original:** The Admin Panel API exposes `register`, `bootstrap`, and `registerTrads` hooks so plugins can inject React UI and translations into Strapi's admin panel.

**中文译文:** Admin Panel API 负责 plugin 的 front-end 部分。Strapi admin panel 是 React application，每个 plugin 都可以通过自己的 admin entry file 注册 React UI、navigation、settings、hooks、reducers、injection zones 与 translations。

## Entry file

**Original:** The entry file is `[plugin-name]/admin/src/index.js|ts`.

**中文译文:** Admin Panel API entry file 通常为：

`[plugin-name]/admin/src/index.js|ts`

主要 lifecycle：
- `register(app)`
- `bootstrap(app)`
- `registerTrads({ locales })`

## `register()`

**Original:** `register()` runs while the plugin is loaded, before admin bootstrap.

**中文译文:** `register()` 在 admin application bootstrap 前执行，适合注册 plugin 自己的基础能力：
- `registerPlugin()`
- Main navigation menu link；
- 新 settings section；
- Injection zones；
- Redux reducers；
- Hooks。

```js
export default {
  register(app) {
    app.registerPlugin({
      id: 'my-plugin',
      name: 'My Plugin',
    });
  },
};
```

## `registerPlugin()`

| Parameter | 中文说明 |
|---|---|
| `id` | Plugin ID |
| `name` | Plugin display name |
| `apis` | 暴露给其他 plugins 的 front-end API |
| `initializer` | Plugin initialization React component |
| `injectionZones` | Plugin 自己声明的 injection zones |
| `isReady` | Plugin readiness，默认 `true` |

```js
app.registerPlugin({
  id: 'my-plugin',
  name: 'My Plugin',
  apis: {},
  initializer:
    MyInitializerComponent,
  injectionZones: {},
  isReady: false,
});
```

## `bootstrap()`

**Original:** `bootstrap()` runs after all plugins have been registered.

**中文译文:** `bootstrap()` 在所有 plugins 已完成 register 后执行，适合扩展其他 plugin 或操作已经存在的 admin extension points：
- `getPlugin()`
- `registerHook()`
- 向现有 settings section 添加 link；
- Content Manager List/Edit view actions；
- Injection components。

```js
export default {
  bootstrap(app) {
    app
      .getPlugin('content-manager')
      .injectComponent(
        'editView',
        'right-links',
        {
          name: 'my-compo',
          Component:
            () => 'my-compo',
        }
      );
  },
};
```

## Available actions

| 目标 | API | Lifecycle |
|---|---|---|
| Main navigation 增加 link | `addMenuLink()` | register |
| 新 settings section | `addSettingsLink(section, links)` | register |
| 现有 settings section 加 link | `addSettingsLink(sectionId, links)` | bootstrap |
| Content Manager side panel | `addEditViewSidePanel()` | bootstrap |
| Document menu action | `addDocumentAction()` | bootstrap |
| Header action | `addDocumentHeaderAction()` | bootstrap |
| Bulk action | `addBulkAction()` | bootstrap |
| 声明 injection zone | `registerPlugin({ injectionZones })` | register |
| 注入 component | `injectComponent()` | bootstrap |
| Redux reducer | `addReducers()` | register |
| 创建 hook | `createHook()` | register |
| 订阅 hook | `registerHook()` | bootstrap |
| Plugin translations | `registerTrads()` | registerTrads |
| Authenticated request | `useFetchClient()` / `getFetchClient()` | Any |

**Original:** Self-hosted admin customizations can access `STRAPI_ADMIN_*` environment variables through `process.env`; Strapi Cloud does not expose them to the admin front end.

**中文译文:** Self-hosted project build admin panel 时，以 `STRAPI_ADMIN_` 为 prefix 的 environment variables 可以通过 `process.env` 暴露给 admin bundle。**Strapi Cloud 不提供这项 front-end exposure**。
