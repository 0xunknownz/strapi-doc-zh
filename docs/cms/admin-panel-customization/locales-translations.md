# 📖 对照翻译：Locales & translations

> Source: `docusaurus/docs/cms/admin-panel-customization/locales-translations.md`  
> Upstream SHA: `012b52dd3b1f55cd1a48c60f57908dadd0596df2`

**Original:** Configure admin panel languages with `config.locales` and override Strapi/plugin strings through `config.translations` or custom translation files.

**中文译文:** Admin panel 可通过 `config.locales` 配置可选界面语言，并通过 `config.translations` 或自定义 translation JSON 覆盖 Strapi / plugin 的 UI 文案。

**Original:** Locales determine available interface languages; translations provide displayed text for keys.

**中文译文:** **Locale** 决定 admin UI 中可选择哪些语言；**translation** 则定义每个 key 在对应 locale 下实际显示的文案。

## Defining locales

**Original:** Set `config.locales` in `/src/admin/app`.

```js title="/src/admin/app.js"
export default {
  config: {
    locales: ["ru", "zh"],
  },
  bootstrap() {},
};
```

**中文译文:** 上例在默认 English 之外加入 Russian 与 Chinese locale。

**Original:** `en` cannot be removed because it is both fallback and first-use default.

**中文译文:** `en` 不能从 build 中移除：
- 某 locale 缺少 translation 时会 fallback 到 English；
- 用户第一次打开 admin panel 时 English 也是默认 interface locale。

## Extending translations

**Original:** Extend keys through `config.translations`.

```js title="/src/admin/app.js"
export default {
  config: {
    locales: ["fr"],
    translations: {
      fr: {
        "Auth.form.email.label": "test",
        Users: "Utilisateurs",
        City: "CITY (FRENCH)",
        Id: "ID french",
      },
    },
  },
  bootstrap() {},
};
```

**中文译文:** `config.translations.<locale>` 可以覆盖 core admin translation keys。

**Original:** Plugin translations are namespaced with the plugin name.

```js
translations: {
  fr: {
    "content-type-builder.plugin.name": "Constructeur de Type-Contenu",
  },
}
```

**中文译文:** 覆盖 plugin translation 时，key 前加 plugin name，例如 `content-type-builder.plugin.name`。

**Original:** Additional JSON files can be placed under `/src/admin/extensions/translations`; make sure locale code exists in `config.locales`.

**中文译文:** 大量自定义 translation 或 Strapi 未打包的 locale，可放入 `/src/admin/extensions/translations`。同时必须把 locale code 加入 `config.locales`。

**Original:** Translation changes require an admin rebuild/restart.

**中文译文:** Translation 会被打入 admin bundle。如果修改后没有生效，请重新启动 development server 或重新 build admin panel。
