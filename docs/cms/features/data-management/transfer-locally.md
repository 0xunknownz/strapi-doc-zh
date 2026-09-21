# 📖 对照翻译：Test a data transfer locally

> Source: `docusaurus/docs/cms/features/data-management/transfer-locally.md`  
> Upstream SHA: `94a2f7ebf16c8bb7cf4439c9d14b9f9367edade5`

**Original:** A fully-worked example of the `strapi transfer` workflow between two local Strapi instances, to get familiar with the command before using it against a remote instance.

**中文译文:** 本页给出两个本地 Strapi instances 之间完整的 `strapi transfer` 示例，帮助你在真正连接 remote instance 前熟悉该 command。

**Original:** The `transfer` command is not intended for transferring data between two local instances. The `export` and `import` commands were designed for this purpose. However, you might want to test `transfer` locally on test instances before using it with a remote instance.

**中文译文:** `transfer` command 的主要用途并不是在两个 local instances 之间传输数据；这种场景更适合使用 `export` 和 `import`。不过，在与 remote instance 配合使用前，可以先通过两个 test instances 在本地练习 `transfer` 流程。

## Create and clone a new Strapi project

**Original:** 1. Create a new Strapi project:

```bash
npx create-strapi-app@latest <project-name> --quickstart
```

**中文译文:** 1. 创建一个新的 Strapi 项目：

```bash
npx create-strapi-app@latest <project-name> --quickstart
```

**Original:** 2. Create at least 1 content type. Do not add data yet.

**中文译文:** 2. 在项目中至少创建 1 个 content type。此时**不要添加任何数据**。如需操作说明，可参考 [Quick Start Guide](/cms/quick-start)。

**Original:** 3. Commit the project to a git repository:

```bash
git init
git add .
git commit -m "first commit"
```

**中文译文:** 3. 将项目提交到 Git repository，命令保持原样：

```bash
git init
git add .
git commit -m "first commit"
```

**Original:** 4. Clone the project repository:

```bash
cd ..
git clone <path to created git repository>.git/ <new-instance-name>
```

**中文译文:** 4. Clone 项目 repository：

```bash
cd ..
git clone <path to created git repository>.git/ <new-instance-name>
```

**Original:** 5. Move into the cloned project and install dependencies.

**中文译文:** 5. 进入 clone 出来的项目并安装 dependencies：

```bash
# yarn
cd <new-instance-name>
yarn install

# npm
cd <new-instance-name>
npm install
```

**Original:** Without this step, the next `build` and `start` commands fail because `strapi` is not yet on the project's local executable path.

**中文译文:** 如果跳过安装 dependencies，后续 `build` 和 `start` 会失败，因为此时 `strapi` 还不在项目的 local executable path 中。

## Add data to the first Strapi instance

**Original:** 1. Return to the first Strapi instance and add data to the content type.
2. Stop the server on the first instance.

**中文译文:** 1. 返回第一个 Strapi instance，并向 content type 添加数据；
2. 停止第一个 instance 的 server。

## Create a transfer token

**Original:** 1. On the second instance, run `build` and `start`:

```bash
# yarn
yarn build && yarn start

# npm
npm run build && npm run start
```

2. Register an admin user.
3. Create and copy a transfer token.
4. Leave the server running.

**中文译文:** 1. 在第二个 instance 根目录运行 `build` 与 `start`：

```bash
# yarn
yarn build && yarn start

# npm
npm run build && npm run start
```

2. 注册 admin user；
3. [创建并复制 transfer token](/cms/features/data-management#admin-panel-settings)；
4. 保持 server 运行。

## Transfer your data

**Original:** 1. Return to the first Strapi instance.
2. Run:

```bash
# yarn
yarn strapi transfer --to http://localhost:1337/admin

# npm
npm run strapi transfer -- --to http://localhost:1337/admin
```

3. When prompted, apply the transfer token.
4. When complete, return to the second instance and verify the content was transferred.

**中文译文:** 1. 返回第一个 Strapi instance；
2. 在 terminal 中运行：

```bash
# yarn
yarn strapi transfer --to http://localhost:1337/admin

# npm
npm run strapi transfer -- --to http://localhost:1337/admin
```

3. 出现 prompt 时输入 transfer token；
4. Transfer 完成后，返回第二个 instance，确认内容已成功传输。

**Original:** If you receive a connection refused error targeting `localhost`, try `http://127.0.0.1:1337/admin`.

**中文译文:** 如果访问 `localhost` 时遇到 connection refused，可以改用 `http://127.0.0.1:1337/admin`。
