# 📖 对照翻译：Sample `.env` files

> Source: `docusaurus/docs/snippets/sample-env.md`  
> Upstream SHA: `2377425268c3111cf4318dce9b6a50e3e2d6a006`

**Original:** The Strapi CLI generates an `.env` and an `.env.example` file when creating a new project. The files contain automatically-generated security keys and database settings similar to the following:

**中文译文:** 使用 Strapi CLI 创建新项目时，会自动生成 `.env` 和 `.env.example` 文件。文件中包含自动生成的 security keys 与 database settings，结构类似下面的示例。

**Original code (kept unchanged):**

```env title=".env.example"
HOST=0.0.0.0
PORT=1337
APP_KEYS="toBeModified1,toBeModified2"
API_TOKEN_SALT=tobemodified
ADMIN_JWT_SECRET=tobemodified
TRANSFER_TOKEN_SALT=tobemodified
JWT_SECRET=tobemodified
ENCRYPTION_KEY=tobemodified
```

**中文译文:** 上面是 `.env.example` 示例。变量名与示例值保持原样。

**Original:** The variables might differ depending on options selected on project creation.

**中文译文:** 实际生成的 variables 可能会根据创建项目时选择的 options 而有所不同。

**Original code (kept unchanged):**

```env title=".env"
# Server
HOST=0.0.0.0
PORT=1337

# Secrets
APP_KEYS=appkeyvalue1,appkeyvalue2,appkeyvalue3,appkeyvalue4
API_TOKEN_SALT=anapitokensalt
ADMIN_JWT_SECRET=youradminjwtsecret
TRANSFER_TOKEN_SALT=transfertokensaltvalue
ENCRYPTION_KEY=yourencryptionkey

# Database
DATABASE_CLIENT=sqlite
DATABASE_HOST=
DATABASE_PORT=
DATABASE_NAME=
DATABASE_USERNAME=
DATABASE_PASSWORD=
DATABASE_SSL=false
DATABASE_FILENAME=.tmp/data.db
```

**中文译文:** 上面是典型 `.env` 示例，包含 Server、Secrets 与 Database variables。代码保持原样。
