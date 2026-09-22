# 📖 对照翻译：Advanced policies for the GraphQL API

> Source: `docusaurus/docs/cms/api/graphql/advanced-policies.md`  
> Upstream SHA: `dcbc143e3c3812b9cb8ed7cd63cad5ca1c60d02d`

**Original:** Policies can be attached to GraphQL resolvers to implement complex authorization rules, such as limiting results for unauthenticated users or restricting access based on group membership.

**中文译文:** GraphQL request 同样会经过 Strapi 的 middleware / policy system。可以把 policy 绑定到 resolver，实现比简单 role permission 更复杂的 authorization，例如限制 anonymous user 返回数量，或根据 group membership 决定是否允许执行 resolver。

## Conditional visibility

**Original:** A policy can modify resolver arguments to limit results for unauthenticated users.

**中文译文:** Policy 不仅可以返回 `true` / `false`，也可以读取并修改 resolver arguments。例如 public user 只允许返回 4 条数据：

```ts title="/src/policies/limit-public-results.ts"
export default async (policyContext, config, { strapi }) => {
  const { state, args } = policyContext;

  if (!state.user) {
    args.limit = 4;
  }

  return true;
};
```

**Original:** Register the policy and attach it to a resolver.

**中文译文:** 然后在 GraphQL policy configuration 中，把 global policy 绑定到目标 resolver：

```ts title="/config/policies.ts"
export default {
  'api::restaurant.restaurant': {
    find: ['global::limit-public-results'],
  },
};
```

**中文译文:** 这样 authenticated user 使用原始 query arguments，而 anonymous user 的 resolver `limit` 会被强制设为 4。

## Group membership

**Original:** Policies can inspect `policyContext.state.user` and query group membership.

**中文译文:** Policy 可以通过 `policyContext.state.user` 获取当前 authenticated user，再查询自定义 group relation：

```ts title="/src/policies/is-group-member.ts"
export default async ({ state }, config, { strapi }) => {
  const userGroups = await strapi
    .query('plugin::users-permissions.group')
    .findMany({
      where: {
        users: {
          id: state.user.id,
        },
      },
    });

  return userGroups.some((g) => g.name === config.group);
};
```

**Original:** Pass a custom group name in the policy configuration.

```ts title="/config/policies.ts"
export default {
  'api::restaurant.restaurant': {
    find: [
      {
        name: 'global::is-group-member',
        config: {
          group: 'editors',
        },
      },
    ],
  },
};
```

**中文译文:** 该 resolver 只有在当前 user 属于 `editors` group 时才返回结果。Policy 的 `config.group` 让同一个 policy 可以复用到多个 group。
