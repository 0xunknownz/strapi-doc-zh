# 📖 对照翻译：Logos

> Source: `docusaurus/docs/cms/admin-panel-customization/logos.md`  
> Upstream SHA: `f96621be455914113d79f93953368be2a775a692`

**Original:** Update login and navigation logos by extending the admin app.

**中文译文:** 可以通过 admin app configuration 替换 login screen 与 main navigation 中的 Strapi logo。

| UI location | Configuration key | 中文说明 |
|---|---|---|
| Login page | `config.auth.logo` | Authentication 页面 logo |
| Main navigation | `config.menu.logo` | Admin panel 左上角 navigation logo |

**Original:** Logos uploaded through admin UI override logos configured in files.

**中文译文:** 通过 admin panel UI 上传的 logo 优先级高于 configuration file 中设置的 logo。

## Updating logos

**Original:** Put image files in `/src/admin/extensions`, import them in `src/admin/app`, and set the two keys.

```jsx title="/src/admin/app.js"
import AuthLogo from "./extensions/my-auth-logo.png";
import MenuLogo from "./extensions/my-menu-logo.png";

export default {
  config: {
    auth: {
      logo: AuthLogo,
    },
    menu: {
      logo: MenuLogo,
    },
  },
  bootstrap() {},
};
```

**中文译文:** 将 asset 放到 `/src/admin/extensions` 后 import，并分别赋值给 `config.auth.logo` 与 `config.menu.logo`。代码保持原样。

**Original:** There is no size limit for image files configured through files.

**中文译文:** 通过 configuration file 设置的 logo 没有 Strapi 强制 image-size limit；实际仍建议控制 bundle size，并优先使用适合 UI 清晰显示的 SVG / optimized asset。
