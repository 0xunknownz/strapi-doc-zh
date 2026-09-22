# 📖 对照翻译：How to create admin permissions from plugins

> Source: `docusaurus/docs/cms/plugins-development/guides/admin-permissions-for-plugins.md`  
> Upstream SHA: `236e968cbf72c13e6014e43db9b454990bfc2367`

**Original:** Plugins can register admin permissions server-side and enforce them in admin pages, menu links, and components.

**中文译文:** Plugin 可以把自己的操作接入 Strapi Admin RBAC。完整流程分两步：
1. Server side 注册 permission actions；
2. Admin side 用 `Page.Protect`、menu link permissions 或 `useRBAC` 执行 UI / page 访问控制。

## Register permissions on the server

**Original:** Permission actions are registered in plugin `bootstrap()` with `actionProvider.registerMany()`.

**中文译文:** Admin permission action 应在 plugin `bootstrap()` 中注册，因为此时 admin permission service 已完成初始化。

```js
const bootstrap =
  ({ strapi }) => {
    const actions = [
      {
        section: 'plugins',
        displayName:
          'Access the overview page',
        uid:
          'overview.access',
        pluginName:
          'my-plugin',
      },
      {
        section: 'plugins',
        displayName:
          'Access the content manager sidebar',
        uid:
          'sidebar.access',
        pluginName:
          'my-plugin',
      },
    ];

    strapi.admin.services
      .permission
      .actionProvider
      .registerMany(actions);
  };

module.exports =
  bootstrap;
```

**中文译文:** 最终 action UID 会形成：

- `plugin::my-plugin.overview.access`
- `plugin::my-plugin.sidebar.access`

## Define reusable permission objects

```js
const pluginPermissions = {
  accessOverview: [
    {
      action:
        'plugin::my-plugin.overview.access',
      subject: null,
    },
  ],

  accessSidebar: [
    {
      action:
        'plugin::my-plugin.sidebar.access',
      subject: null,
    },
  ],
};

export default
  pluginPermissions;
```

## Protect a page

```jsx
import {
  Page,
} from '@strapi/strapi/admin';

<Page.Protect
  permissions={
    pluginPermissions
      .accessOverview
  }
>
  <Main>
    ...
  </Main>
</Page.Protect>
```

**中文译文:** `Page.Protect` 会在用户直接访问 URL 时检查 permission，而不是只隐藏 navigation link。

## Protect a menu link

```js
app.addMenuLink({
  to:
    `plugins/${PLUGIN_ID}`,

  icon:
    PluginIcon,

  intlLabel: {
    id:
      `${PLUGIN_ID}.plugin.name`,
    defaultMessage:
      PLUGIN_ID,
  },

  Component:
    () =>
      import('./pages/App'),

  permissions: [
    pluginPermissions
      .accessOverview[0],
  ],
});
```

**中文译文:** Menu link permission 只控制 navigation visibility，因此应与真正 page protection 配合。

## Fine-grained checks with `useRBAC`

```jsx
import {
  useRBAC,
} from '@strapi/strapi/admin';

const {
  allowedActions: {
    canAccessSidebar,
  },
} =
  useRBAC(
    pluginPermissions
  );

if (
  !canAccessSidebar
) {
  return null;
}
```

**中文译文:** `useRBAC` 适合 component-level conditional rendering，例如只对有 permission 的 user 显示 sidebar action/button。
