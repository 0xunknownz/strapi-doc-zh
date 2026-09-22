# 📖 对照翻译：Server API — Configuration

> Source: `docusaurus/docs/cms/plugins-development/server-configuration.md`  
> Upstream SHA: `2761f9f22791279254ca049f95eaffe8a49074a5`

**Original:** A plugin can expose default configuration and a validator. Strapi deep-merges user overrides, validates them, then stores the final config.

**中文译文:** Plugin Server API 可以暴露 `config` object：
- `default`：plugin 默认配置；
- `validator`：验证合并后的最终配置。

Strapi 会先计算 defaults，再与 application 的 `config/plugins.js|ts` deep-merge，然后执行 validator。

## Configuration shape

| Property | 中文说明 |
|---|---|
| `default` | Object，或接收 `{ env }` 并返回 Object 的 function |
| `validator` | 接收 merged config；发现非法值时抛 error |

## Loading sequence

**中文译文:**
1. 计算 plugin default；
2. Deep-merge 用户配置，user value 优先；
3. 执行 `validator(mergedConfig)`；
4. Validation 通过后保存到 plugin instance。

## Example

```js title="/src/plugins/my-plugin/server/src/config/index.js"
module.exports = {
  default: ({ env }) => ({
    enabled: true,
    maxItems: env.int('MY_PLUGIN_MAX_ITEMS', 10),
    endpoint: env(
      'MY_PLUGIN_ENDPOINT',
      'https://api.example.com'
    ),
  }),

  validator: (config) => {
    if (typeof config.enabled !== 'boolean') {
      throw new Error('"enabled" must be a boolean');
    }

    if (
      typeof config.maxItems !== 'number' ||
      config.maxItems < 1
    ) {
      throw new Error(
        '"maxItems" must be a positive number'
      );
    }
  },
};
```

**Original:** Application overrides live in `config/plugins.js|ts`.

```js
module.exports = {
  'my-plugin': {
    enabled: true,
    config: {
      maxItems: 25,
      endpoint: 'https://api.production.example.com',
    },
  },
};
```

## Runtime access

```js
const maxItems =
  strapi.plugin('my-plugin').config('maxItems');

const pluginConfig =
  strapi.config.get('plugin::my-plugin');
```

**中文译文:** 推荐在 lifecycle / controller / service 方法执行时读取 config，而不是 module load time 提前缓存。

## Best practices

**中文译文:**
- 总是提供合理 defaults；
- Environment-aware value 使用 `default: ({ env }) => ...`；
- Validator error 应明确指出具体字段；
- 不要把 raw secret 硬编码进 plugin config；
- Runtime 使用最终 merged config，而不是 initialization 前 snapshot。
