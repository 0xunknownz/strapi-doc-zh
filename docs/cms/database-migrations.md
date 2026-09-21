# 📖 对照翻译：Database migrations

> Source: `docusaurus/docs/cms/database-migrations.md`  
> Upstream SHA: `ef4a6126e4048256fcfd0fd7d9ed39623536d46c`

**Original:** Database migrations run one-time scripts before the schema sync to preserve data during upgrades. Migration files export an `up()` function and run once, in alphabetical order. During the schema sync that follows, Strapi drops the tables, columns, indexes, and foreign keys it previously managed that are no longer in the content-types schemas.

**中文译文:** Database migrations 会在 schema sync 之前运行一次性脚本，用于在升级过程中保存或转换数据。Migration file 导出 `up()` function，并按照文件名 alphabetical order 每个只执行一次。随后 schema sync 会删除 Strapi 以前管理、但已经不再出现在 content-types schemas 中的 tables、columns、indexes 和 foreign keys。

**Original:** Database migrations exist to run one-time queries against the database, typically to modify table structure or data when upgrading a Strapi application. They run automatically on application startup, before Strapi's automated schema sync.

**中文译文:** Database migration 用于对 database 执行一次性 queries，常见用途是在升级 Strapi application 时修改 table structure 或转换 data。Application 启动时会自动执行 migrations，并且执行顺序早于 Strapi 自动 schema sync。

**Original:** Database migrations are experimental.

**中文译文:** Database migrations 目前属于 **Experimental feature**，仍在持续完善。如果遇到问题，可以通过 GitHub Discussions 或 Strapi Discord 社区寻求帮助。

## Understanding database migration files

**Original:** Migrations are JavaScript files stored in `./database/migrations`. Strapi detects new files and runs each once at the next startup in alphabetical order.

**中文译文:** Migration 使用存放在 `./database/migrations` 中的 JavaScript files。Strapi 会自动检测新 migration file，并在下一次启动时按 alphabetical order 执行；每个新文件只会执行一次。

### What happens on startup

**Original:** On every startup:
1. Strapi loads schemas and converts content-types/components into database models, then validates relations.
2. Strapi runs pending migrations, first project migrations then internal migrations. Each runs in its own transaction and applied migrations are tracked.
3. Strapi syncs database schema, creating tables/columns, dropping tables no longer in schemas, then altering remaining tables.
4. Strapi persists the resulting schema as the reference for the next startup.

**中文译文:** 每次启动时，Strapi 按以下顺序处理：
1. 加载 schema：将 content-types 与 components 转换为 database models，并验证 relations；
2. 执行 pending migrations：先执行 `/database/migrations` 中的项目 migration，再执行 Strapi internal migrations。每个 migration 在独立 transaction 中运行，并记录已执行状态，避免重复执行；
3. 同步 database schema：比较 content-types schemas 与 database 差异，先创建 tables / columns，再删除 schema 中已不存在的 tables，最后修改其余 tables；
4. 持久化新 schema：把最终 schema 保存到 database，作为下一次启动的 reference。

**Original:** Migrations run before schema sync, so `up()` sees the database in its previous state. Write migrations against the old schema.

**中文译文:** Migration 在 schema sync **之前**执行，因此 `up()` 看到的是 database 的旧状态。Migration code 应针对**旧 schema** 编写，而不是目标新 schema。

**Original:** If there is no pending migration and schemas have not changed, migration and schema sync steps are skipped. Strapi compares content-type schemas, not the live database, so manual DB changes are not detected or reverted.

**中文译文:** 如果没有 pending migration，并且 content-types schemas 自上次启动以来没有变化，则 migration 与 schema sync 都会跳过。Strapi 判断变化时比较的是 content-types schemas，而不是直接检查 database，因此手动在 database 中进行的修改不会被自动检测或还原。

### Data loss during schema sync

**Original:** Schema sync automatically drops Strapi-managed tables, columns, indexes, and foreign keys that no longer match content-type schemas, with no warning or confirmation, in both development and production. Deleting a content type from code deletes its table/data on next startup.

**中文译文:** Schema sync 会自动删除 Strapi 曾经管理、但已不再匹配 content-type schema 的 tables、columns、indexes 和 foreign keys。此操作在 Development 与 Production 中行为一致，并且**没有 warning 或 confirmation prompt**。因此，从代码中删除 content-type 后，下一次启动会删除对应 table 及其 data。

**Original:** Tables Strapi never managed, such as manually created DB tables, are left untouched. Use migrations to copy or transform data before schema sync removes old structures.

**中文译文:** Strapi 从未管理过的 tables（例如直接在 database 中手工创建的 table）不会受影响。若 schema change 可能删除旧结构，应使用 migration 在 schema sync 前复制或转换 data，以避免丢失。

**Original:** Strapi does not support down migrations. Reverts must be manual.

**中文译文:** Strapi 当前**不支持 down migration**。如果需要回滚 migration，必须手动处理；官方计划支持 down migration，但目前没有时间表。

**Original:** `forceMigration=false` skips drop operations. The new schema is still recorded, so skipped objects stop being tracked and won't later be dropped when the flag is turned back on. `runMigrations` controls project migration files only and does not affect schema sync.

**中文译文:** Database configuration 中将 `forceMigration` 设置为 `false` 可以跳过所有 drop operations。但新 schema 仍会被记录为 reference，因此本次被跳过删除的 object 将不再由 Strapi 追踪；以后即使重新设为 `true`，也不会再自动 drop。另一个参数 `runMigrations` 只控制 `/database/migrations` 中的自定义 migration files 是否运行，**不会影响 schema sync**。

**Original:** Migration files export `up()`. It runs in a transaction; if a query fails, the migration is rolled back. Nested transactions behave as nested transactions.

**中文译文:** Migration file 应导出 `up()`。该 function 在 database transaction 中运行；如果其中 query 失败，整个 migration 会取消，不会把部分修改写入 database。如果 migration 内部再创建 transaction，则作为 nested transaction 运行。

**Original:** There is no CLI to manually execute database migrations.

**中文译文:** 当前没有用于手动执行 database migrations 的 CLI command。

## Creating a migration file

**Original:** 1. Create a dated migration file in `./database/migrations`, e.g. `2022.05.10T00.00.00.name-of-my-migration.js`. Filename ordering defines execution order.
2. Use this template:

```jsx
'use strict'

async function up(knex) {}

module.exports = { up };
```

3. Add migration logic in `up()`. It receives a Knex instance already inside a transaction.

**中文译文:** 创建 migration：
1. 在 `./database/migrations` 中创建以日期和 migration name 命名的文件，例如 `2022.05.10T00.00.00.name-of-my-migration.js`。务必遵循命名格式，因为 alphabetical order 决定执行顺序；
2. 使用下面的模板；
3. 在 `up()` 内加入实际 migration logic。`up()` 接收已经处于 transaction 状态的 Knex instance，可直接执行 database queries。

**Original code (kept unchanged):**

```jsx title="./database/migrations/2022.05.10T00.00.00.name-of-my-migration.js"
module.exports = {
  async up(knex) {
    await knex.schema.renameTable('oldName', 'newName');

    await knex.schema.table('someTable', table => {
      table.renameColumn('oldName', 'newName');
    });

    await knex.from('someTable').update({ columnName: 'newValue' }).where({ columnName: 'oldValue' });
  },
};
```

**中文译文:** 示例展示 rename table、rename column 与 update data；代码保持原样。

### Using Strapi Instance for migrations

**Original:** If you use the Strapi instance instead of Knex directly, wrap migration code in `strapi.db.transaction()`; otherwise errors may not roll back correctly.

**中文译文:** 如果 migration 不直接使用 Knex，而是调用 Strapi instance，应把 migration code 包在 `strapi.db.transaction()` 中，否则发生 error 时 migration 可能无法正确 rollback。

**Original code (kept unchanged):**

```jsx title="./database/migrations/2022.05.10T00.00.00.name-of-my-migration.js"
module.exports = {
  async up() {
    await strapi.db.transaction(async () => {
      await strapi.documents('api::article.article').create({
        data: {
          title: 'My Article',
        },
      });

      await strapi.service('api::article.article').updateRelatedArticles();
    });
  },
};
```

**中文译文:** 示例通过 Document Service 创建 entry，并调用 custom service；代码保持原样。

## Reading migration progress heartbeats

**Original:** Some internal migrations run for minutes. They log a progress heartbeat at most every 60 seconds, for example:
`[document-id] still running (120s) · articles 12000/450000`

**中文译文:** 某些 Strapi internal migration 会处理大量数据，可能持续数分钟。为了表明任务仍在运行，Strapi 最多每 60 秒输出一条 progress heartbeat，例如：
`[document-id] still running (120s) · articles 12000/450000`。
Prefix 表示正在执行的 internal migration，counter 表示已处理 rows 数量。这些信息会追加到 logs，而不是原地刷新。

**Original:** Progress heartbeats are only for Strapi internal migrations, not custom migration files.

**中文译文:** Progress heartbeat 仅由 Strapi internal migrations 输出，自定义 migration files 不支持。

## Handling migrations with TypeScript code

**Original:** By default Strapi looks for migration files in the source directory, so TypeScript migrations won't run unless Strapi is configured to use the build directory.

**中文译文:** TypeScript 项目中，Strapi 默认仍在 source directory 查找 migration files，因此 TypeScript migration 如果不额外配置，可能无法被正确发现和执行。

**Original:** Set `useTypescriptMigrations: true` in database settings to look in the build directory.

**中文译文:** 在 database configuration 中设置 `useTypescriptMigrations: true`，让 Strapi 从 build directory 查找 migrations。

**Original code (kept unchanged):**

```js title="/config/database.js"
module.exports = ({ env }) => ({
  connection: {
    // Your database connection settings
  },
  settings: {
    useTypescriptMigrations: true
  }
});
```

```ts title="/config/database.ts"
export default ({ env }) => ({
  connection: {
    // Your database connection settings
  },
  settings: {
    useTypescriptMigrations: true
  }
});
```

**中文译文:** JavaScript / TypeScript database configuration 示例保持原样。

**Original:** To keep using existing JavaScript migrations alongside TypeScript migrations, set `allowJs: true` in `tsconfig.json`.

**中文译文:** 如果希望 TypeScript migrations 与已有 JavaScript migrations 并存，可在 `tsconfig.json` compiler options 中设置 `allowJs: true`。
