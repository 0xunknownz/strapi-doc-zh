# 📖 对照翻译：How to access and cast environment variables

> Source: `docusaurus/docs/cms/configurations/guides/access-cast-environment-variables.md`  
> Upstream SHA: `e50d0655f6220bcd7e92838fc613fc334d65fba2`

**Original:** The `env()` utility accesses environment variables from `.env` files and casts them to `int`, `float`, `bool`, `json`, `array`, `date`, and `oneOf`.

**中文译文:** Strapi configuration factory 中的 `env()` utility 用于读取 environment variable，并可转换为 integer、float、boolean、JSON、array、date 或枚举值。

**Original:** Store environment-specific values such as database credentials in `.env` rather than hard-coding them in config files.

**中文译文:** Database credentials、provider secrets 等 environment-specific / sensitive values 应放在 project root 的 `.env`，而不是硬编码到 configuration source。

```dotenv title=".env"
DATABASE_PASSWORD=acme
```

**Original:** Override the `.env` path with `ENV_PATH`.

```bash
ENV_PATH=/absolute/path/to/.env npm run start
```

**中文译文:** 如需加载其他位置的 environment file，可在启动前设置 `ENV_PATH`。

## Accessing values

**Original:** Variables can always be read from `process.env`. In config factories, prefer `env()` for defaults and casting.

**中文译文:** 任何 application code 都可以通过 `process.env.VARIABLE_NAME` 读取变量；configuration factory 中更推荐使用 `env()`，因为它支持 default value 与类型转换。

```js title="./config/database.js"
module.exports = ({ env }) => ({
  connections: {
    default: {
      settings: {
        password: env('DATABASE_PASSWORD'),
      },
    },
  },
});
```

**Original:** `env('VAR', 'default-value')` returns the default when the variable is undefined.

**中文译文:** `env('VAR', 'default-value')` 在环境变量未定义时返回 default value。

## Casting

```js
env('VAR', 'default');
env.int('VAR', 0);
env.float('VAR', 3.14);
env.bool('VAR', true);
env.json('VAR', { key: 'value' });
env.array('VAR', [1, 2, 3]);
env.date('VAR', new Date());
env.oneOf('UPLOAD_PROVIDER', ['local', 'aws'], 'local');
```

**中文译文:**
- `env()`：string / raw value；
- `env.int()`：使用 `parseInt`；
- `env.float()`：使用 `parseFloat`；
- `env.bool()`：判断值是否为字符串 `'true'`；
- `env.json()`：通过 `JSON.parse`；
- `env.array()`：解析 array syntax；
- `env.date()`：创建 `Date`；
- `env.oneOf()`：只允许预定义 union values。
