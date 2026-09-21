# 📖 对照翻译：Cloud notifications

> Source: `docusaurus/docs/cloud/projects/notifications.md`  
> Upstream SHA: `efc64b652220e255b1707bb50fc010159caacf22`

**Original:** Cloud notifications

**中文译文:** Cloud 通知

**Original:** Bell icon opens a feed of recent deployment events, automatically purged after 30 days.

**中文译文:** 点击铃铛图标可以打开最近 deployment 事件的通知列表；超过 30 天的通知会自动清除。

**Original:** The Notification center can be opened by clicking the bell icon in the top navigation of the Cloud dashboard.

**中文译文:** 点击 Cloud dashboard 顶部导航中的铃铛图标，即可打开 Notification center。

**Original:** It displays a list of the latest notifications for all your existing projects. Clicking on a notification card from the list will redirect you to the *Log details* page of the corresponding deployment.

**中文译文:** Notification center 会显示所有现有项目的最新通知列表。点击其中某张通知卡片，会跳转到对应 deployment 的 *Log details* 页面。更多信息请参阅 [Deploy history & logs](/cloud/projects/deploys-history#accessing-deployment-details--logs)。

**Original:** The following notifications can be listed in the Notifications center:

- *deployment completed*: when a deployment is successfully done.
- *Build failed*: when a deployment fails during the build stage.
- *deployment failed*: when a deployment fails during the deployment stage.
- *deployment triggered*: when a deployment is triggered by a new push to the connected repository. This notification is however not sent when the deployment is triggered manually.

**中文译文:** Notifications center 中可能出现以下通知：

- *deployment completed*：deployment 成功完成；
- *Build failed*：deployment 在 build 阶段失败；
- *deployment failed*：deployment 在 deployment 阶段失败；
- *deployment triggered*：连接的 repository 收到新的 push，从而触发 deployment。手动触发 deployment 时不会发送这类通知。

**Original:** All notifications older than 30 days are automatically removed from the Notification center.

**中文译文:** 超过 30 天的通知会自动从 Notification center 中删除。
