# 📖 对照翻译：Push a Strapi project to GitHub

> Source: `docusaurus/docs/snippets/push-to-github.md`  
> Upstream SHA: `8b9d52e90702173073093b94be73a5bfbb79aa55`

**Original:** Steps required to push your Strapi project code to GitHub:

**中文译文:** 将 Strapi 项目代码推送到 GitHub 所需的步骤：

**Original:**
1. In the terminal, ensure you are in the folder that hosts the Strapi project you created.
2. Run the `git init` command to initialize git for this folder.
3. Run the `git add .` command to add all modified files to the git index.
4. Run the `git commit -m "Initial commit"` command to create a commit with all the added changes.
5. Log in to your GitHub account and create a new repository. Give the new repository a name, for instance `my-strapi-project`, and remember this name.
6. Go back to the terminal and push your local repository to GitHub.

**中文译文:**
1. 在终端中确认当前目录就是你所创建的 Strapi 项目目录。
2. 运行 `git init`，为该目录初始化 Git 仓库。
3. 运行 `git add .`，将所有已修改文件加入 Git index。
4. 运行 `git commit -m "Initial commit"`，把已经加入 index 的变更创建为一次 commit。
5. 登录 GitHub 账户并创建一个新仓库。为新仓库命名，例如 `my-strapi-project`，并记住这个名称。
6. 返回终端，将本地仓库推送到 GitHub。

**Original:** Run a command similar to the following: `git remote add origin git@github.com:yourname/my-strapi-project.git`, ensuring you replace `yourname` by your own GitHub profile name, and `my-strapi-project` by the actual name you used at step 5.

**中文译文:** 运行类似下面的命令：`git remote add origin git@github.com:yourname/my-strapi-project.git`。请将 `yourname` 替换为你自己的 GitHub 用户名，并将 `my-strapi-project` 替换为第 5 步实际创建的仓库名称。

**Original:** Run the `git push --set-upstream origin main` command to finally push the commit to your GitHub repository.

**中文译文:** 运行 `git push --set-upstream origin main`，将 commit 推送到你的 GitHub 仓库。

**Original:** Additional information about using git with the command line interface can be found in the official GitHub documentation.

**中文译文:** 关于通过命令行使用 Git 的更多信息，请参阅 GitHub 官方文档。
