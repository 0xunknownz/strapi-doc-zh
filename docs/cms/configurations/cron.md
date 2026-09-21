# 📖 对照翻译：Cron jobs

> Source: `docusaurus/docs/cms/configurations/cron.md`  
> Upstream SHA: `a467485b6f666efc9c83efbce91e99f0afffb12a`

**Original:** Cron jobs schedule custom functions at specific times via `node-schedule`, activated through server config and optional task files.

**中文译文:** Cron jobs 基于 `node-schedule` 在指定时间执行自定义 function，通过 server configuration 启用，并可使用独立 task file 定义任务。

**Original:** Prerequisite: set `cron.enabled` to `true` in `./config/server.js` or `./config/server.ts`.

**中文译文:** 前置条件：需要在 `./config/server.js` 或 TypeScript 项目的 `./config/server.ts` 中将 `cron.enabled` 设置为 `true`。

**Original:** `cron` schedules arbitrary functions at specific dates with optional recurrence rules. It uses a single timer rather than reevaluating jobs every second/minute. It is powered by `node-schedule`.

**中文译文:** `cron` 可以按指定 date 执行任意 function，并可设置 recurrence rules。它在任意时刻只使用一个 timer，而不是每秒 / 每分钟重新扫描 upcoming jobs。底层由 `node-schedule` package 提供能力。

**Original:** Cron format:

```text
*    *    *    *    *    *
┬    ┬    ┬    ┬    ┬    ┬
│    │    │    │    │    |
│    │    │    │    │    └ day of week (0 - 7) (0 or 7 is Sun)
│    │    │    │    └───── month (1 - 12)
│    │    │    └────────── day of month (1 - 31)
│    │    └─────────────── hour (0 - 23)
│    └──────────────────── minute (0 - 59)
└───────────────────────── second (0 - 59, OPTIONAL)
```

**中文译文:** Cron expression 从左到右依次为：second（可选）、minute、hour、day of month、month、day of week。原格式示意保持不变。

**Original:** To use cron jobs: create the task file, then enable jobs in server configuration. Jobs may also be declared directly in `cron.tasks`.

**中文译文:** 使用 cron jobs 的基本流程：
1. 创建 cron task file；
2. 在 server configuration 中启用 cron jobs。
也可以直接在 server configuration 的 `cron.tasks` 中声明任务。

## Creating a cron job

**Original:** A cron job can use object format or key format.

**中文译文:** Cron job 可以使用 object format 或 key format；官方更推荐 object format。

### Using the object format

**Original code (kept unchanged):**

```js title="./config/cron-tasks.js"
module.exports = {
  myJob: {
    task: ({ strapi }) => {
      // Add your own logic here
    },
    options: {
      rule: "0 0 1 * * 1",
    },
  },
};
```

```ts title="./config/cron-tasks.ts"
export default {
  myJob: {
    task: async ({ strapi }) => {
      // Add your own logic here
    },
    options: {
      rule: "0 0 1 * * 1",
    },
  },
};
```

**中文译文:** 示例定义 `myJob`，每周一凌晨 1 点运行。JavaScript / TypeScript 代码保持原样。

#### Timezone example

**Original:** Add `tz` to run a job in a specific timezone.

**中文译文:** 可以在 `options` 中添加 `tz`，让 cron job 按指定 timezone 执行，例如：

```js
options: {
  rule: "0 0 1 * * 1",
  tz: "Asia/Dhaka",
}
```

#### One-off cron jobs

**Original:** A Date object can be used as `options` to run once at a given time.

**中文译文:** 如果只希望执行一次，可以直接把 `Date` object 作为 `options`：

```js
options: new Date(Date.now() + 10000)
```

该示例在约 10 秒后执行一次。

#### Start and end times

**Original:** Recurring jobs can define `start` and `end` dates.

**中文译文:** Recurring cron job 可以同时指定 `start` 与 `end`：

```js
options: {
  rule: "* * * * * *",
  start: new Date(Date.now() + 10000),
  end: new Date(Date.now() + 20000),
}
```

### Using the key format

**Original:** Key format creates an anonymous cron job and can cause problems disabling jobs or with plugins; object format is recommended.

**中文译文:** Key format 会创建 anonymous cron job，可能导致后续 disable job 或与某些 plugins 配合时出现问题，因此建议优先使用 object format。

**Original code (kept unchanged):**

```js title="./config/cron-tasks.js"
module.exports = {
  "0 0 1 * * 1": ({ strapi }) => {
    // Add your own logic here
  },
};
```

```ts title="./config/cron-tasks.ts"
export default {
  "0 0 1 * * 1": async ({ strapi }) => {
    // Add your own logic here
  },
};
```

**中文译文:** Key 本身就是 cron rule，以上示例每周一凌晨 1 点执行。代码保持原样。

## Enabling cron jobs

**Original:** Set `cron.enabled=true` and provide tasks in server configuration.

**中文译文:** 在 server configuration 中设置 `cron.enabled: true`，并加载 tasks。

**Original code (kept unchanged):**

```js title="./config/server.js"
const cronTasks = require("./cron-tasks");

module.exports = ({ env }) => ({
  host: env("HOST", "0.0.0.0"),
  port: env.int("PORT", 1337),
  cron: {
    enabled: true,
    tasks: cronTasks,
  },
});
```

```ts title="./config/server.ts"
import cronTasks from "./cron-tasks";

export default ({ env }) => ({
  host: env("HOST", "0.0.0.0"),
  port: env.int("PORT", 1337),
  cron: {
    enabled: true,
    tasks: cronTasks,
  },
});
```

**中文译文:** JavaScript 与 TypeScript server configuration 示例保持原样。

## Adding or removing cron jobs

**Original:** Use `strapi.cron.add` in custom code to add jobs.

**中文译文:** 可以在 custom code 中调用 `strapi.cron.add` 动态添加 cron job：

```js title="./src/plugins/my-plugin/strapi-server.js"
module.exports = () => ({
  bootstrap({ strapi }) {
    strapi.cron.add({
      myJob: {
        task: ({ strapi }) => {
          console.log("hello from plugin");
        },
        options: {
          rule: "* * * * * *",
        },
      },
    });
  },
});
```

**Original:** Use `strapi.cron.remove("myJob")` to remove a named job. Jobs using the key-as-rule format cannot be removed.

**中文译文:** 使用 `strapi.cron.remove("myJob")` 可以删除指定 key 的 cron job。采用 key-as-rule format 的 anonymous cron job 无法通过这种方式删除。

## Listing cron jobs

**Original:** Use `strapi.cron.jobs` to list currently running jobs.

**中文译文:** 在 custom code 中访问 `strapi.cron.jobs` 可以列出当前运行中的 cron jobs：

```js
strapi.cron.jobs
```
