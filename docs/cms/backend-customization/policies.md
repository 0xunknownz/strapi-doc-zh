# 📖 对照翻译：Policies

> Source: `docusaurus/docs/cms/backend-customization/policies.md`  
> Upstream SHA: `6a1adf2451dc8ef9ed2ae2cc35a7b9891550e91a`

**Original:** Policies execute before controllers to enforce authorization or other checks on routes.

**中文译文:** Policy 是在 request 到达 controller 之前执行的 validation / authorization function，最常见用途是保护 business logic 与限制 route access。

**Original:** Each route can have an array of policies. A policy such as `is-admin` can block non-admin access.

**中文译文:** 每个 route 都可以配置一个 policies array。例如 `is-admin` policy 可以检查当前 user 是否为 administrator，不满足时阻止 request 到达 controller。

**Original:** Policies can be global or scoped to an API/plugin.

**中文译文:** Policy 可以有不同 scope：
- Global policy：可被项目任意 route 引用；
- API policy：只定义在特定 API namespace 下；
- Plugin policy：由 plugin 定义并暴露。

## Implementation

**Original:** Create policies with `strapi generate` or manually in:
- `./src/policies/`
- `./src/api/[api-name]/policies/`
- `./src/plugins/[plugin-name]/policies/`

**中文译文:** 可以通过 `strapi generate` 创建，也可以手动放置到：
- `./src/policies/`：global；
- `./src/api/[api-name]/policies/`：API-scoped；
- `./src/plugins/[plugin-name]/policies/`：plugin-scoped。

### Global policy example

```js
module.exports = (policyContext, config, { strapi }) => {
  if (policyContext.state.user) {
    return true;
  }

  return false;
};
```

**中文译文:** Policy 返回 `true` 时允许继续执行下一 policy / controller；显式返回 `false` 时阻止 request。注意：如果什么都不 return，Strapi 会认为没有阻止 request。

**Original:** `policyContext` wraps controller context and adds logic useful across REST and GraphQL.

**中文译文:** `policyContext` 是 controller context 的 wrapper，提供适合在 REST / GraphQL 共同使用的 policy context。

### Configurable policy

```js
module.exports = (policyContext, config, { strapi }) => {
  if (policyContext.state.user.role.code === config.role) {
    return true;
  }

  return false;
};
```

**中文译文:** Policy 可通过 route 中的 config 接收参数。上例把当前 user role 与 `config.role` 比较，从而让同一个 policy 支持不同 route 配置。

## Usage

**Original:** Apply policies in route configuration.

**中文译文:** 在 route 的 `config.policies` 中声明需要执行的 policies。

**Original:** Naming:
- `global::policy-name`
- `api::api-name.policy-name`
- `plugin::plugin-name.policy-name`

**中文译文:** 引用 naming：
- Global：`global::policy-name`；
- API：`api::api-name.policy-name`；
- Plugin：`plugin::plugin-name.policy-name`。

**Original:** Run `yarn strapi policies:list` to list available policies.

**中文译文:** 可运行 `yarn strapi policies:list` 查看所有已注册 policies。

### Global policy route example

```js
module.exports = {
  routes: [
    {
      method: 'GET',
      path: '/restaurants',
      handler: 'Restaurant.find',
      config: {
        policies: ['global::is-authenticated']
      }
    }
  ]
}
```

**中文译文:** 上例在执行 `Restaurant.find` 前调用 global `is-authenticated` policy。

### Plugin policy example

```js
module.exports = {
  routes: [
    {
      method: 'GET',
      path: '/restaurants',
      handler: 'Restaurant.find',
      config: {
        policies: ['plugin::users-permissions.isAuthenticated']
      }
    }
  ]
}
```

**中文译文:** Plugin policy 使用 `plugin::` namespace。上例引用 Users & Permissions plugin 提供的 authentication policy。

### API policy example

```js
module.exports = async (policyContext, config, { strapi }) => {
  if (policyContext.state.user.role.name === 'Administrator') {
    return true;
  }

  return false;
};
```

**中文译文:** API policy 可以放在 `./src/api/restaurant/policies/is-admin.js`，并通过 route 中 `policies: ['is-admin']` 引用。

**Original:** To reference a policy defined in another API, use `api::[apiName].[policyName]`.

**中文译文:** 如果要跨 API 使用 policy，需写完整 UID，例如 `api::restaurant.is-admin`。
