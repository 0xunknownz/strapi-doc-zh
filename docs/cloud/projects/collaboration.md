# 📖 对照翻译：Cloud project collaboration

> Source: `docusaurus/docs/cloud/projects/collaboration.md`  
> Upstream SHA: `48cc30836df595e596c329612d7cc7e30b7b9934`

**Original:** Cloud project collaboration

**中文译文:** Cloud 项目协作

**Original:** Project owners invite maintainers through the Share button, manage pending invitations, and revoke access.

**中文译文:** Project owner 可以通过 **Share** 邀请 maintainers、管理待处理邀请，并撤销访问权限。

**Original:** Projects are created by a user via their Strapi Cloud account. Strapi Cloud users can share their projects to anyone else, so these new users can have access to the project dashboard and collaborate on that project, without the project owner to ever have to share their credentials.

**中文译文:** 项目由用户通过自己的 Strapi Cloud 账户创建。Strapi Cloud 用户可以把项目共享给其他人，让受邀用户访问项目 dashboard 并参与协作，而 project owner 无需共享自己的账户凭据。

**Original:** Users invited to collaborate on a project, called maintainers, do not have the same permissions as the project owner. Contrary to the project owner, maintainers:

- Cannot share the project themselves to someone else
- Cannot delete the project from the project settings
- Cannot access the *Billing* section of project settings

**中文译文:** 被邀请参与项目协作的用户称为 maintainers，他们拥有的权限与 project owner 不同。与 project owner 相比，maintainers：

- 不能继续把项目共享给其他人；
- 不能从项目设置中删除项目；
- 不能访问项目设置中的 *Billing* 区域。

## Sharing a project

**Original:** To invite a new maintainer to collaborate on a project:

1. From the *Projects* page, click on the project of your choice to be redirected to its dashboard.
2. Click on the **Share** button located in the dashboard's header.
3. In the *Share [project name]* dialog, type the email address of the person to invite in the textbox. A dropdown indicating "Invite [email address]" should appear.
4. Click on the dropdown: the email address should be displayed in a purple box right below the textbox.
5. (optional) Repeat steps 3 and 4 to invite more people. Email addresses can only entered one by one but invites can be sent to several email addresses at the same time.
6. Click on the **Send** button.

**中文译文:** 邀请新的 maintainer 参与项目协作：

1. 在 *Projects* 页面选择目标项目，进入其 dashboard。
2. 点击 dashboard header 中的 **Share**。
3. 在 *Share [project name]* 对话框的文本框中输入受邀者邮箱地址。此时应出现 “Invite [email address]” 下拉项。
4. 点击该下拉项；邮箱地址会以紫色标签显示在文本框下方。
5. （可选）重复第 3、4 步邀请更多用户。邮箱地址需要逐个输入，但可以一次向多个地址发送邀请。
6. 点击 **Send**。

**Original:** New maintainers will be sent an email containing a link to click on to join the project. Once a project is shared, avatars representing the maintainers will be displayed in the project dashboard's header, next to the **Share** button, to see how many maintainers collaborate on that project and who they are.

**中文译文:** 新的 maintainers 会收到一封邮件，其中包含加入项目的链接。项目共享后，dashboard header 的 **Share** 按钮旁会显示 maintainers 的头像，方便查看当前有哪些用户参与协作以及人数。

**Original:** Avatars use GitHub, Google or GitLab profile pictures, but for pending users only initials will be displayed until the activation of the maintainer account. You can hover over an avatar to display the full name of the maintainer.

**中文译文:** 头像会使用 GitHub、Google 或 GitLab 的 profile picture。对于仍处于 pending 状态的用户，在 maintainer 账户激活前只会显示姓名首字母。将鼠标悬停在头像上，可以查看 maintainer 的完整姓名。

## Managing maintainers

**Original:** From the *Share [project name]* dialog accessible by clicking on the **Share** button of a project dashboard, projects owners can view the full list of maintainers who have been invited to collaborate on the project. From there, it is possible to see the current status of each maintainer and to manage them.

**中文译文:** 在项目 dashboard 中点击 **Share**，打开 *Share [project name]* 对话框后，project owner 可以查看所有已受邀参与项目协作的 maintainers，并查看每位 maintainer 的当前状态与执行管理操作。

**Original:** Maintainers whose full name is displayed are users who did activate their account following the invitation email. If however there are maintainers in the list whose email address is displayed, it means they haven't activated their accounts and can't access the project dashboard yet. In that case, a status should be indicated right next to the email address to explain the issue:

- Pending: the invitation email has been sent but the maintainer hasn't acted on it yet.
- Expired: the email has been sent over 72 hours ago and the invitation expired.

**中文译文:** 如果列表中显示 maintainer 的完整姓名，说明该用户已经通过邀请邮件激活账户。如果列表中仍显示邮箱地址，则表示账户尚未激活，目前还不能访问项目 dashboard。此时邮箱旁会显示状态：

- Pending：邀请邮件已发送，但 maintainer 尚未处理；
- Expired：邀请邮件发送已超过 72 小时，邀请已过期。

**Original:** For Expired statuses, it is possible to send another invitation email by clicking on the **Manage** button, then **Resend invite**.

**中文译文:** 对于状态为 Expired 的用户，可以点击 **Manage**，然后选择 **Resend invite**，重新发送邀请邮件。

### Revoking maintainers

**Original:** To revoke a maintainer's access to the project dashboard:

1. Click on the **Share** button in the project dashboard's header.
2. In the list of *People with access*, find the maintainer whose access to revoke and click on the **Manage** button.
3. Click on the **Revoke** button.
4. In the confirmation dialog, click again on the **Revoke** button.

**中文译文:** 要撤销某位 maintainer 对项目 dashboard 的访问权限：

1. 点击项目 dashboard header 中的 **Share**。
2. 在 *People with access* 列表中找到目标 maintainer，并点击 **Manage**。
3. 点击 **Revoke**。
4. 在确认对话框中再次点击 **Revoke**。

**Original:** The revoked maintainer will completely stop having access to the project dashboard.

**中文译文:** 权限被撤销后，该 maintainer 将彻底失去对项目 dashboard 的访问权限。

**Original:** Maintainers whose access to the project has been revoked do not receive any email or notification.

**中文译文:** 项目访问权限被撤销的 maintainer 不会收到邮件或其他通知。
