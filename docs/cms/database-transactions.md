# 📖 对照翻译：Database transactions

> Source: `docusaurus/docs/cms/database-transactions.md`  
> Upstream SHA: `8ec9345db00b9b74826626b8686f48f69dc74792`

**Original:** Database transactions group several operations so they succeed or roll back as a unit. The experimental `strapi.db.transaction` helper exposes `trx`, commit, and rollback utilities.

**中文译文:** Database transaction 把多个 database operations 作为一个不可分割的 unit 执行：全部成功则 commit；任意一步失败则整体 rollback。Strapi 5 提供 experimental `strapi.db.transaction()` helper。

**Original:** This feature is experimental.

**中文译文:** **该 API 当前属于 experimental feature**，后续版本可能变化。

## Basic usage

**Original:** Pass an async handler to `strapi.db.transaction`.

```js
await strapi.db.transaction(async ({ trx, rollback, commit, onCommit, onRollback }) => {
  const article = await strapi.documents('api::article.article').create({
    data: { title: 'My Article', slug: 'my-article' },
  });

  await strapi.documents('api::log.log').create({
    data: { action: 'article_created', targetId: article.documentId },
  });
});
```

**中文译文:** Handler 正常完成时 transaction 自动 commit；任何 operation 抛错时自动 rollback。

**Original:** Document Service, Query Engine, and Entity Service calls inside a transaction implicitly use it through AsyncLocalStorage.

**中文译文:** Transaction block 内执行的：
- Document Service API；
- `strapi.db.query`；
- legacy `strapi.entityService`

都会通过 Node.js `AsyncLocalStorage` 自动继承 transaction context，因此无需手工传 `trx`。

## Handler properties

| Property | 中文说明 |
|---|---|
| `trx` | Knex transaction object |
| `commit` | 显式 commit function |
| `rollback` | 显式 rollback function |
| `onCommit` | 注册 commit 完成后执行的 callback |
| `onRollback` | 注册 rollback 后执行的 callback |

## Nested transactions

**Original:** Nested transactions implicitly use the outer transaction and resolve with the outer commit/rollback.

**中文译文:** Transaction 可以嵌套。Inner transaction 会继承 outer transaction context，最终随 outer transaction 一起 commit / rollback。

```js
await strapi.db.transaction(async () => {
  await strapi.documents('api::article.article').create({
    data: { title: 'My Article', slug: 'my-article' },
  });

  await strapi.db.transaction(async () => {
    await strapi.documents('api::category.category').create({
      data: { name: 'Tech' },
    });
  });
});
```

## `onCommit` / `onRollback`

**Original:** Hooks can run side effects after the transaction has actually committed or rolled back.

**中文译文:** `onCommit` / `onRollback` 适合把 side effect 延后到 transaction outcome 已确定之后，例如：
- Commit 后发 welcome email；
- Rollback 后记录 failure log。

## Knex queries

**Original:** Raw Knex queries must explicitly call `.transacting(trx)`.

**中文译文:** 与 Strapi data APIs 不同，raw Knex query 不会自动绑定 transaction object，必须显式调用：

```js
await strapi.db.transaction(async ({ trx }) => {
  await knex('users')
    .where('id', 1)
    .update({ name: 'foo' })
    .transacting(trx);
});
```

## When to use

**Original:** Use transactions when multiple dependent database operations must succeed or fail together.

**中文译文:** 适合 transaction 的场景：多个 database writes 互相依赖，并且业务上要求原子性。

**Original:** Avoid transactions for independent operations because they add performance costs and locking risk.

**中文译文:** 不相关 operations 不应强行放进同一 transaction，因为会增加：
- DB locking；
- Connection 占用；
- Latency；
- Deadlock / long-running transaction 风险。

**Original:** Transactions can stall if code paths fail to close them correctly.

**中文译文:** Transaction 使用不当可能导致长期未 commit / rollback 的连接，造成 blocking 或 instability。应尽量缩短 transaction scope，并避免在 transaction 内执行耗时外部 I/O。
