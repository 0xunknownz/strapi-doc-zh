# 📖 对照翻译：Cloud deployments management

> Source: `docusaurus/docs/cloud/projects/deploys.md`  
> Upstream SHA: `e37fa7f105ec29c22735f71221a6e699886e0518`

**Original:** Cloud deployments management

**中文译文:** Cloud deployment 管理

**Original:** Deployment triggers can be manual or automatic on git pushes, with the ability to cancel active builds from dashboard or CLI.

**中文译文:** Deployment 既可以手动触发，也可以在 Git push 时自动触发；正在进行的 build 还可以通过 dashboard 或 CLI 取消。

**Original:** The creation of a new Strapi Cloud project automatically trigger the deployment of that project. After that, deployments can be:

- manually triggered whenever needed, from the Cloud dashboard or from the CLI,
- or automatically triggered everytime a new commit is pushed to the branch, if the Strapi Cloud project is connected to a git repository and the "deploy on push" option is enabled.

**中文译文:** 创建新的 Strapi Cloud 项目时，会自动触发该项目的首次 deployment。之后，deployment 可以通过以下方式触发：

- 在需要时手动触发，可以从 [Cloud dashboard](#triggering-a-new-deployment) 或 [CLI](/cloud/cli/cloud-cli#strapi-deploy) 操作；
- 如果 Strapi Cloud 项目已连接 Git repository，并启用了 **deploy on push**，则每次向指定 branch 推送新 commit 时都会自动触发 deployment。相关设置请参阅 [Project settings](/cloud/projects/settings#modifying-git-repository--branch)。

**Original:** Ongoing deployments can also be manually canceled if needed.

**中文译文:** 如有需要，正在进行中的 deployment 也可以手动取消。

## Triggering a new deployment

**Original:** To manually trigger a new deployment for your project, click on the **Trigger deployment** button always displayed in the right corner of a project dashboard's header. This action will add a new card in the *Deployments* tab, where you can monitor the status and view the deployment logs live.

**中文译文:** 如果要手动触发新的 deployment，请点击项目 dashboard header 右侧始终显示的 **Trigger deployment**。操作后，*Deployments* 标签页会新增一张 deployment 卡片，你可以在这里监控状态，并实时查看 deployment logs。更多信息请参阅 [Deploy history and logs](/cloud/projects/deploys-history)。

## Cancelling a deployment

**Original:** If for any reason you want to cancel an ongoing and unfinished deployment:

1. Go to the *Deployment details* page of the latest triggered deployment.
2. Click on the **Cancel deployment** button in the top right corner. The status of the deployment will automatically change to *Canceled*.

**中文译文:** 如果需要取消仍在进行且尚未完成的 deployment：

1. 打开最近一次触发的 deployment 的 *Deployment details* 页面，详见 [Accessing log details](/cloud/projects/deploys-history#accessing-deployment-details--logs)。
2. 点击右上角的 **Cancel deployment**。该 deployment 的状态会自动变为 *Canceled*。

**Original:** You can also cancel a deployment from the *Deployments* tab which lists the deployments history. The card of ongoing deployment with the *Building* status will display a Cancel button for cancelling the deployment.

**中文译文:** 也可以直接在显示 deployment history 的 *Deployments* 标签页中取消 deployment。处于 *Building* 状态的进行中 deployment 卡片会显示 Cancel 按钮，可直接执行取消操作。
