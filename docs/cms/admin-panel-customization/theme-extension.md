# 📖 对照翻译：Theme extension

> Source: `docusaurus/docs/cms/admin-panel-customization/theme-extension.md`  
> Upstream SHA: `c148bfea8077b3461b0c7338a28f15ee83a5172c`

**Original:** Extend light and dark admin themes through `config.theme.light` and `config.theme.dark`.

**中文译文:** Strapi admin panel 同时支持 Light / Dark mode，可分别通过：
- `config.theme.light`
- `config.theme.dark`
扩展对应 theme。

**Original:** Strapi Design System exposes theme keys such as colors and shadows that can be overridden.

**中文译文:** Strapi Design System 的默认 theme 定义了 colors、shadows 等 design tokens，可以在 admin app configuration 中覆盖。

**Original code (kept unchanged):**

```js title="/src/admin/app.js"
export default {
  config: {
    theme: {
      light: {
        colors: {
          primary600: "#4A6EFF",
        },
      },
      dark: {
        colors: {
          primary600: "#9DB2FF",
        },
      },
    },
  },
  bootstrap() {},
}
```

**中文译文:** 上例分别覆盖 Light / Dark mode 的 `primary600`。可根据 Strapi Design System theme keys 扩展其他 tokens。
