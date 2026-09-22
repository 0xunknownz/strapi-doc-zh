# 📖 对照翻译：Advanced queries for the GraphQL API

> Source: `docusaurus/docs/cms/api/graphql/advanced-queries.md`  
> Upstream SHA: `d2ee3723a65dab36ed2d3207c9677ca1ccf1e6a5`

**Original:** Advanced queries use nested selection sets to fetch multi-level relations and custom resolver chains to reuse logic across resolvers and apply context-specific behavior.

**中文译文:** GraphQL plugin 可以自动解析大部分 query，但复杂场景可能需要 multi-level relation selection 或 custom resolver chaining。Nested selection set 用于深层 relation；custom resolver 则可以插入特定业务逻辑并复用 generated resolver。

## Multi-level queries

**Original:** Use nested GraphQL selection sets to fetch multiple relation levels.

```graphql
{
  restaurants {
    documentId
    name
    categories {
      documentId
      name
      parent {
        documentId
        name
      }
    }
  }
}
```

**中文译文:** 上例从 restaurant 获取 categories，并继续向下查询每个 category 的 parent。GraphQL plugin 会自动解析这些 nested relations。

**Original:** If custom logic is needed at a specific level, create a custom resolver for that field.

**中文译文:** 如果某一级 relation 需要额外 authorization、transformation 或 external data，应为对应 field 添加 custom resolver，而不是把整个 query 都改成手写数据访问。

## Resolver chains

**Original:** Custom resolvers can call generated resolvers to reuse default behavior.

**中文译文:** Custom resolver 可以先执行自己的 fetch / permission logic，再委托给 GraphQL plugin 生成的 resolver，复用默认 field-selection 等行为。

```js title="/src/api/restaurant/resolvers/restaurant.ts"
export default {
  Query: {
    restaurants: async (parent, args, ctx) => {
      const documents = await strapi
        .documents('api::restaurant.restaurant')
        .findMany(args);

      return documents.map((doc) =>
        ctx.request.graphql.resolve('Restaurant', doc)
      );
    },
  },
};
```

**中文译文:** 该例：
1. Parent resolver 使用 Document Service API 查询 restaurants；
2. 对每个 document 调用 generated `Restaurant` resolver；
3. 因而保留 GraphQL plugin 的标准 field resolution 行为。

**Original:** GraphQL aggregations are not yet implemented in `@strapi/plugin-graphql`.

**中文译文:** 当前 `@strapi/plugin-graphql` 尚未提供通用 GraphQL aggregation API。需要 aggregation 时应参考 GraphQL advanced use cases 中的替代方案。
