# 📖 对照翻译：Cloud deployment history and logs

> Source: `docusaurus/docs/cloud/projects/deploys-history.md`  
> Upstream SHA: `d83b4377d25e6c900e9d63bcae7ac64ded8d72d6`

**Original:** Cloud deployment history and logs

**中文译文:** Cloud deployment 历史与日志

**Original:** Deployments tab lists every build with status and allows deep inspection of build and deployment logs.

**中文译文:** *Deployments* 标签页会列出每次 build 及其状态，并支持深入查看 build logs 和 deployment logs。

**Original:** For each Strapi Cloud project, you can access the history of all deployments that occurred and their details including build and deployment logs. This information is available in the *Deployments* tab.

**中文译文:** 对每个 Strapi Cloud 项目，都可以查看全部历史 deployments 及其详细信息，包括 build logs 和 deployment logs。这些信息位于 *Deployments* 标签页。

## Viewing the deployment history

**Original:** In the *Deployments* tab is displayed a chronological list of cards with the details of all historical deployments for your project.

**中文译文:** *Deployments* 标签页会按时间顺序显示项目所有历史 deployments 的卡片及详细信息。

**Original:** Each card displays the following information:

- Commit SHA, with a direct link to your git provider, and commit message
- Deployment status:
  - *Deploying*
  - *Done*
  - *Canceled*
  - *Build failed*
  - *Deployment failed*
- Last deployment time (when the deployment was triggered and the duration)
- Branch

**中文译文:** 每张卡片都会显示以下信息：

- Commit SHA，以及跳转到 Git provider 的直接链接和 commit message。Commit SHA（或 hash）是 commit 的唯一 ID，用于标识某一时间点发生的一次具体变更；
- Deployment 状态：
  - *Deploying*
  - *Done*
  - *Canceled*
  - *Build failed*
  - *Deployment failed*
- 最近 deployment 时间，包括触发时间和持续时长；
- Branch。

## Accessing deployment details & logs

**Original:** From the *Deployments* tab, you can hover a deployment card to make the **Show details** button appear. Clicking on this button will redirect you to the *Deployment details* page which contains the deployment's detailed logs.

**中文译文:** 在 *Deployments* 标签页中，将鼠标悬停在 deployment 卡片上会显示 **Show details**。点击后会进入 *Deployment details* 页面，其中包含该 deployment 的详细日志。

**Original:** In the *Build logs* and *Deployment logs* sections of the page you can click on the arrow buttons to show or hide the build and deployment logs of the deployment.

**中文译文:** 在页面的 *Build logs* 和 *Deployment logs* 区域，可以通过箭头按钮展开或收起本次 deployment 的 build logs 与 deployment logs。

**Original:** Click the **Copy to clipboard** button to copy the log contents.

**中文译文:** 点击 **Copy to clipboard** 可以复制日志内容。

**Original:** In the right side of the *Deployment details* page is also displayed the following information:

- *Commit*: the commit SHA, with a direct link to your git provider, and commit message used for this deployment
- *Status*, which can be *Building*, *Deploying*, *Done*, *Canceled*, *Build failed*, or *Deployment failed*
- *Source*: the branch and commit message for this deployment
- *Duration*: the amount of time the deployment took and when it occurred

**中文译文:** *Deployment details* 页面右侧还会显示以下信息：

- *Commit*：本次 deployment 使用的 commit SHA、跳转到 Git provider 的直接链接，以及 commit message；
- *Status*：可能为 *Building*、*Deploying*、*Done*、*Canceled*、*Build failed* 或 *Deployment failed*；
- *Source*：本次 deployment 对应的 branch 和 commit message；
- *Duration*：deployment 的持续时间及发生时间。
