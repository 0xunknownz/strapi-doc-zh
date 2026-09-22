# 📖 对照翻译：How to access configuration values from code

> Source: `docusaurus/docs/cms/configurations/guides/access-configuration-values.md`  
> Upstream SHA: `5de07dc920bd3458e9b1007339cbec578725352e`

**Original:** Access configuration values loaded on startup using `strapi.config.get()` with dot notation for nested keys across all configuration files.

**中文译文:** Strapi startup 时会加载全部 configuration files。运行过程中可以通过 `strapi.config.get()` 与 dot notation 读取任意已加载配置。

**Original:** Given `config/server.js` with `host: '0.0.0.0'`, access it through `strapi.config.get('server.host')`.

**中文译文:** 例如：

```js title="./config/server.js"
module.exports = {
  host: '0.0.0.0',
};
```

读取方式：

```js
strapi.config.get('server.host', 'defaultValueIfUndefined');
```

**Original:** The configuration filename becomes the first prefix.

**中文译文:** Configuration filename 会成为 key prefix。例如：
- `config/server.js` → `server.*`
- `config/plugins.js` → `plugins.*`
- 自定义 `config/foo.js` → `foo.*`

**Original:** Config files may be `.js`, `.ts`, or `.json`.

**中文译文:** Configuration file 可以使用 `.js`、`.ts` 或 `.json`。

## Export forms

**Original:** JS/TS config can export an object.

```js
module.exports = {
  mySecret: 'someValue',
};
```

**中文译文:** 简单配置可以直接 export object。

**Original:** Recommended: export a function receiving `env`.

```js
module.exports = ({ env }) => {
  return {
    mySecret: env('MY_SECRET_KEY', 'defaultSecretValue'),
  };
};
```

**中文译文:** 更推荐 export configuration factory，因为可以使用 `env` utility，为不同 deployment environment 注入变量和默认值。
