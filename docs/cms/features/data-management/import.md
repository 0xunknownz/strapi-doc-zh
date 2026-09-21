# 📖 对照翻译：Data import

> Source: `docusaurus/docs/cms/features/data-management/import.md`  
> Upstream SHA: `0a1f9cfe32ac68e6d4339cf194d7e04bcd001191`

**Original:** The `strapi import` command restores project data from an encrypted or compressed archive, including content, configuration, files, and schemas. It supports importing from `.tar.gz.enc` files or unpacked directories, with options to exclude or include specific data types.

**中文译文:** `strapi import` command 用于从 encrypted / compressed archive 恢复项目数据，包括 content、configuration、files 和 schemas。它既支持 `.tar.gz.enc` 文件，也支持未打包目录，并可通过 options 选择排除或仅导入特定数据类型。

**Original:** By default, `strapi import` imports project configuration, entities, links, assets, schemas, and `metadata.json` from an encrypted and compressed `tar.gz.enc` file.

**中文译文:** 默认情况下，`strapi import` 会从 encrypted + compressed 的 `tar.gz.enc` 中导入：
- project configuration；
- entities；
- links（entities 之间的 relations）；
- assets（uploads 文件）；
- schemas；
- `metadata.json`。

**Original:** The archive follows the same structure as `strapi export`. Compression and encryption are detected from extensions; plain `.tar` and unpacked export directories are also supported.

**中文译文:** Import archive 使用与 [`strapi export`](/cms/features/data-management/export) 相同的结构。Compression（`.gz`）和 encryption（`.enc`）会根据扩展名自动识别；也可以 import 普通 `.tar` 或 unpacked export directory。

**Original:** Warnings:
- `strapi import` deletes all existing database data and uploads before importing.
- Source and target schemas must match.
- Admin users are not restored, so `createdBy` and `updatedBy` are empty.
- With cloud storage providers, media whose DB records are removed can be permanently deleted remotely; isolate storage between environments.

**中文译文:** 重要警告：
- `strapi import` 在 import backup 前会删除现有 database data 与 uploads；
- Source 与 target schemas 必须匹配，所有 content types 应一致；
- Restore 不包含 Admin users table，因此 restored instance 中 `createdBy` 与 `updatedBy` 会为空；
- 如果使用 Cloudinary、AWS S3、Azure Blob Storage、Google Cloud Storage 等 cloud storage provider，import 时被删除 database record 对应的 media 可能通过 provider delete API 从远端永久删除；共享同一 storage account 的多个 environments 都可能受影响，因此应为不同 environment 使用隔离 bucket/account。

## Understand the import archive

**Original:** Expected structure:
- `configuration/`: project config
- `entities/`: entity records
- `links/`: relations
- `schemas/`: schema definitions
- `metadata.json`: export metadata
Each folder contains JSONL records.

**中文译文:** Import archive 应包含：
- `configuration/`：project configuration；
- `entities/`：entity records；
- `links/`：entity relations；
- `schemas/`：schema definitions；
- `metadata.json`：export metadata。
各目录包含一个或多个 `.jsonl` 文件，每行一条 record，便于 import 前人工修改或转换数据。

### Asset metadata validation

**Original:** Starting with Strapi 5.54.0+, each `assets/uploads` file must have a matching JSON sidecar under `assets/metadata`. Before modifying the destination, import validates that sidecars exist, contain valid JSON objects with required fields, and match upload filenames.

**中文译文:** Strapi 5.54.0+ 中，`assets/uploads` 下每个文件都必须在 `assets/metadata` 中拥有匹配的 JSON sidecar。Import 在修改 destination 前会执行 preflight validation，检查 sidecar 是否存在、是否为合法 JSON object、是否包含 restore 所需 fields，以及 sidecar 记录的 filename 是否与 upload 对应。

**Original:** Invalid archives are rejected before existing data is backed up or deleted. Strapi does not repair missing metadata or match assets by filename/hash. Validation is skipped if assets are excluded.

**中文译文:** 如果 archive 未通过检查，会在现有数据 backup 或 delete 前直接拒绝，因此 destination 会保持原样。该检查只是 preflight，不负责修复：Strapi 不会重建缺失 metadata，也不会按 filename/hash 自动匹配 assets。若通过 `--exclude files` 或 `--only` 排除 assets，则跳过该检查。

**Original code (kept unchanged):**

```bash
# Yarn
yarn strapi export --no-encrypt --no-compress -f my-export
tar -xf my-export.tar

# NPM
npm run strapi export -- --no-encrypt --no-compress -f my-export
tar -xf my-export.tar
```

**中文译文:** 可以先按上面的方式生成未加密、未压缩 export 并解包，人工修改 `.jsonl` 后重新使用 `tar -cf my-export.tar configuration entities links schemas metadata.json` 打包，再执行 `strapi import -f my-export.tar`。Encryption / compression 会根据扩展名自动识别。

## Import from a directory

**Original:** Pass an unpacked export directory produced by `strapi export --format dir`. Encryption and compression are skipped automatically.

**中文译文:** 可以直接把 [`strapi export --format dir`](/cms/features/data-management/export#export-to-a-directory) 生成的 unpacked export directory 传给 import。目录应包含 `metadata.json`、`schemas/`、`entities/`、`links/`、`configuration/`，以及可选 `assets/`。Directory import 会自动跳过 encryption / compression。

```bash
# Yarn
yarn strapi import -f ./my-export

# NPM
npm run strapi import -- -f ./my-export
```

## Specify the import file

**Original:** Run `strapi import` from the destination project root and use `-f` or `--file` for the archive/directory path. Encrypted files prompt for the key.

**中文译文:** 在 destination project root 运行 `strapi import`，并使用 `-f` 或 `--file` 指定 archive / directory。Archive import 必须包含完整 filename、extension 和 path；encrypted file 会在开始前要求 encryption key。

```bash
# Encrypted archive — Yarn
yarn strapi import -f /path/to/my/file/export_20221213105643.tar.gz.enc

# Encrypted archive — NPM
npm run strapi import -- -f /path/to/my/file/export_20221213105643.tar.gz.enc

# Plain tar — Yarn
yarn strapi import -f /path/to/my/file/backup.tar

# Plain tar — NPM
npm run strapi import -- -f /path/to/my/file/backup.tar
```

## Provide an encryption key

**Original:** Use `-k` or `--key` to pass the encryption key.

**中文译文:** 对 encrypted file，可用 `-k` / `--key` 直接传入 encryption key：

```bash
# Yarn
yarn strapi import -f /path/to/my/file/export_20221213105643.tar.gz.enc --key my-encryption-key

# NPM
npm run strapi import -- -f /path/to/my/file/export_20221213105643.tar.gz.enc --key my-encryption-key
```

## Bypass all command line prompts

**Original:** Import requires confirmation because it deletes existing database contents. `--force` bypasses the prompt, useful for programmatic imports. Encrypted files also need `--key`.

**中文译文:** Import 会删除现有 database contents，因此默认要求确认。使用 `--force` 可以跳过 prompt，适合 programmatic import；如果文件 encrypted，还必须同时传入 `--key`。

```bash
# Yarn
yarn strapi import -f /path/to/my/file/export_20221213105643.tar.gz.enc --force --key my-encryption-key

# NPM
npm run strapi import -- -f /path/to/my/file/export_20221213105643.tar.gz.enc --force --key my-encryption-key
```

## Exclude data types during import

**Original:** `--exclude` can exclude `content`, `files`, and `config`. Schemas cannot be excluded. Stages omitted through `--exclude` or `--only` are preserved in the target; imported stages fully replace corresponding target data.

**中文译文:** `--exclude` 可以排除 `content`、`files` 和 `config`；schemas 不能排除。通过 `--exclude` 或 `--only` 跳过的 stage 不会在 target instance 中被 wipe，其已有数据会保留；真正被 import 的 stage 会完整替换 target 中对应数据。

**Original:** Excluding asset files does not exclude their database records, so media links can break.

**中文译文:** Media 同时包含 asset file 和 database entity。使用 `--exclude files` 排除 assets 时，database records 仍可能被 import，因此可能出现 broken links。

```bash
# Yarn
yarn strapi import -f /path/to/my/file/export_20221213105643.tar.gz.enc --exclude files

# NPM
npm strapi import -- -f /path/to/my/file/export_20221213105643.tar.gz.enc --exclude files
```

## Include only specified data types

**Original:** `--only` accepts `content`, `files`, and `config`; schemas are always imported.

**中文译文:** `--only` 可以只 import 指定类型，可用值为 `content`、`files`、`config`，多个值用无空格逗号分隔。Schemas 始终 import，因为 `strapi import` 依赖 schema matching。

```bash
# Yarn
yarn strapi import -f /path/to/my/file/export_20221213105643.tar.gz.enc --only config

# NPM
npm strapi import -- -f /path/to/my/file/export_20221213105643.tar.gz.enc --only config
```

## Filter content types during import

**Original:** `--exclude-content-types` and `--only-content-types` accept comma-separated content-type UIDs.

**中文译文:** `--exclude-content-types` 与 `--only-content-types` 支持传入逗号分隔的 content-type UIDs，例如 `api::article.article`。Unknown UID 会在启动时根据 Strapi schema 验证。

**Original:** Restore behavior:
- With `--exclude-content-types`, excluded type data is preserved on the destination.
- With `--only-content-types`, pre-import wiping is restricted to listed UIDs, leaving all others untouched.

**中文译文:** Restore 行为：
- 使用 `--exclude-content-types` 时，被排除类型的数据在 destination 中**保留**，import 不会在 restore 前删除它们；
- 使用 `--only-content-types` 时，pre-import wipe 只针对列出的 UIDs，其他 content 保持不变。

```bash
# Exclude one type — Yarn
yarn strapi import -f export_20221213105643.tar.gz.enc --exclude-content-types api::article.article

# Exclude one type — NPM
npm run strapi import -- -f export_20221213105643.tar.gz.enc --exclude-content-types api::article.article

# Only specific types — Yarn
yarn strapi import -f export_20221213105643.tar.gz.enc --only-content-types api::article.article,api::category.category

# Only specific types — NPM
npm run strapi import -- -f export_20221213105643.tar.gz.enc --only-content-types api::article.article,api::category.category
```
