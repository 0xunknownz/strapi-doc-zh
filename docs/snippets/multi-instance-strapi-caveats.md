# 📖 对照翻译：Multi-instance Strapi caveats

> Source: `docusaurus/docs/snippets/multi-instance-strapi-caveats.md`  
> Upstream SHA: `84a8746cc415cbe1b7f84cda384c6a0eec9426cb`

**Original:** Multiple Strapi processes sharing one database need extra care around schema synchronization, migrations, cron, in-memory state, and local uploads.

**中文译文:** 多 instance / cluster 模式下，多个 Strapi process 共用同一个 database 时需要额外注意 schema sync、migration、cron、in-memory state 与 local upload。

**Original:** Schema sync runs once per process and has no lock shared across instances.

**中文译文:** 每个 process 启动时都会执行 schema synchronization，而且 instances 之间没有全局 lock。Content-types 未变化时通常安全；但**包含 schema change 或 pending migration 的 release 不应同时启动多个 instance**。

**Original:** Roll a single instance first for schema-changing releases, then start the others after it finishes booting.

**中文译文:** 对包含 schema / migration 变更的部署，应先只启动一个 instance，等待其完整 bootstrap / migration 完成，再逐个启动其他 instances。

**Original:** Cron jobs run once per instance.

**中文译文:** Strapi cron task 是 process-local scheduler，所以 3 个 instances 会让同一 nightly job 执行 3 次。需要“全局只执行一次”的任务应移出 Strapi，或只在一个 instance 启用 cron。

**Original:** In-memory state is not replicated.

**中文译文:** 每个 instance 都有独立 memory；Strapi core 不会自动同步 process-local state。

**Original:** Local upload uses each instance's disk.

**中文译文:** Local upload provider 将文件写入当前 instance disk。跨主机 / container 的多 instance 部署应改用 object storage provider。
