# 📖 对照翻译：Data export

> Source: `docusaurus/docs/cms/features/data-management/export.md`  
> Upstream SHA: `2f43a6cb89535138e0c63a0cd904e39307327cd1`

**Original:** The `strapi export` command exports data from a Strapi instance as an encrypted and compressed archive containing entities, relations, assets, schemas, and configuration. Customize exports using options like `--no-encrypt`, `--no-compress`, `--only`, and `--exclude`.

**中文译文:** `strapi export` command 会把 Strapi instance 中的数据导出为经过 encryption 与 compression 的 archive，其中包含 entities、relations、assets、schemas 和 configuration。可以使用 `--no-encrypt`、`--no-compress`、`--only`、`--exclude` 等 options 自定义导出内容。

**Original:** By default, `strapi export` creates an encrypted and compressed `tar.gz.enc` file containing project configuration, entities, links, assets, schemas, and `metadata.json`.

**中文译文:** 默认情况下，`strapi export` 会生成经过 encryption 与 compression 的 `tar.gz.enc` 文件，包含：
- project configuration；
- entities：全部内容；
- links：entities 之间的 relations；
- assets：uploads 目录中的文件；
- schemas；
- `metadata.json`。

**Original:** Admin users and API tokens are not exported.

**中文译文:** Admin users 与 API tokens **不会**被导出。

## Understand the exported archive

**Original:** The exported `.tar` archive contains numbered JSON Lines files grouped by resource:

```text
export_202401011230.tar
├── metadata.json
├── configuration/
│   └── configuration_00001.jsonl
├── entities/
│   └── entities_00001.jsonl
├── links/
│   └── links_00001.jsonl
└── schemas/
    └── schemas_00001.jsonl
```

**中文译文:** 导出的 `.tar` archive 按 resource 分目录保存编号的 JSON Lines 文件，目录结构如上，代码保持原样。

**Original:** Each folder except `metadata.json` contains one or more sequential `.jsonl` files. Each line is a single record. Export without compression/encryption to inspect files directly.

**中文译文:** 除 `metadata.json` 外，每个目录包含一个或多个按序号命名的 `.jsonl` 文件，例如 `entities_00001.jsonl`。每一行代表一条 record，便于逐行处理或转换为 CSV。若要直接检查内容，可关闭 compression 和 encryption。

**Original code (kept unchanged):**

```bash
# Yarn
yarn strapi export --no-encrypt --no-compress -f my-export

# NPM
npm run strapi export -- --no-encrypt --no-compress -f my-export
```

**中文译文:** 上述 command 会在项目根目录生成 `my-export.tar`。使用 `tar -xf my-export.tar` 解压后，可直接打开 `.jsonl` 文件查看 records。大型 dataset 会自动拆分到多个 `.jsonl` 文件，单文件最大大小由 `maxSizeJsonl` provider option 控制。

## Export to a directory

**Original:** By default, `strapi export` produces a `.tar` archive. Use `--format dir` to write an unpacked directory with the same layout. Directory exports do not support encryption or compression, and `--no-encrypt` must be passed explicitly.

**中文译文:** 默认输出为 `.tar` archive。使用 `--format dir` 可以直接输出未打包目录，目录结构与 archive 相同。Directory export 不支持 encryption 或 compression，并且必须显式传入 `--no-encrypt`。

```bash
# Yarn
yarn strapi export --format dir --no-encrypt -f my-export

# NPM
npm run strapi export -- --format dir --no-encrypt -f my-export
```

**Original:** Directory format is useful for version control because JSON and JSONL files show as regular text diffs.

**中文译文:** Directory format 很适合提交到 version control；JSON 与 JSONL 会以普通文本 diff 的形式展示，更容易在 pull request 中检查变更。

## Name the export file

**Original:** Exports are automatically named `export_YYYYMMDDHHMMSS`. Use `--file` or `-f` to choose a name. Do not include an extension for archive exports.

**中文译文:** Export 默认使用 `export_YYYYMMDDHHMMSS` 命名。可以通过 `--file` 或 `-f` 指定名称。Archive export 不要手动添加扩展名，扩展名会根据 options 自动设置；directory export 中 `-f` 的值就是输出目录路径。

```bash
# Yarn
yarn strapi export --file my-strapi-export

# NPM
npm run strapi export -- --file my-strapi-export
```

## Configure data encryption

**Original:** The default export uses `aes-128-ecb` and adds `.enc`. Supply an encryption key with `-k` or `--key`, or enter one when prompted. The key is a string with no minimum character count.

**中文译文:** 默认 export 使用 `aes-128-ecb` encryption，并添加 `.enc` 扩展名。可以通过 `-k` / `--key` 提供 encryption key，或在 prompt 中输入。Key 类型为 string，没有最小字符数限制。

**Original:** Strong encryption keys are recommended. Example commands:

```bash
# Mac/Linux
openssl rand -base64 48

# Windows
node -p "require('crypto').randomBytes(48).toString('base64');"
```

**中文译文:** 建议使用足够强的 encryption key。以上 command 可用于生成随机 key，代码保持原样。

**Original:** Disable encryption with `--no-encrypt`.

**中文译文:** 使用 `--no-encrypt` 关闭 encryption：

```bash
# Yarn
yarn strapi export --no-encrypt

# NPM
npm run strapi export -- --no-encrypt
```

**Original:** Use `--key my-encryption-key` to provide a key.

**中文译文:** 使用 `--key my-encryption-key` 直接传入 encryption key：

```bash
# Yarn
yarn strapi export --key my-encryption-key

# NPM
npm run strapi export -- --key my-encryption-key
```

## Disable data compression

**Original:** By default, `strapi export` uses `gzip` compression and adds `.gz`. Disable it with `--no-compress`.

**中文译文:** 默认使用 `gzip` compression 并添加 `.gz`。使用 `--no-compress` 可以关闭：

```bash
# Yarn
yarn strapi export --no-compress

# NPM
npm run strapi export -- --no-compress
```

## Export only selected types of data

**Original:** `--only` exports only listed types. Values are `content`, `files`, and `config`. Schemas are always exported.

**中文译文:** `--only` 只导出列出的类型，可用值为 `content`、`files`、`config`，多个值使用无空格逗号分隔。Schemas 始终会导出，因为 `strapi import` 需要进行 schema matching。

**Original:** Media consists of both an asset file and a database entity. If you export only content, asset database records remain and may become broken links.

**中文译文:** 图片等 media 同时由 asset file 与 database entity 组成。如果只导出 `content`，asset 的 database records 仍会保留，但可能变成 broken links。

```bash
# Yarn
yarn strapi export --only content

# NPM
npm run strapi export -- --only content
```

## Exclude items from export

**Original:** `--exclude` can exclude content, files, and project configuration. Schemas cannot be excluded.

**中文译文:** `--exclude` 可以排除 content、files 和 project configuration；schemas 不能排除。

**Original:** Excluding files does not remove their database records and may produce broken media links.

**中文译文:** 排除 files 并不会删除对应 database records，因此 media links 可能失效。

```bash
# Yarn
yarn strapi export --exclude files,content

# NPM
npm run strapi export -- --exclude files,content
```

## Filter content types during export

**Original:** `--exclude-content-types` and `--only-content-types` scope export to content-type UIDs such as `api::article.article`. Unknown UIDs are validated at startup. Entity records and relation links involving excluded types are skipped.

**中文译文:** `--exclude-content-types` 和 `--only-content-types` 可按 content-type UID 控制 export scope，例如 `api::article.article`。Unknown UID 会在启动时依据 Strapi schema 校验；被排除类型的 entity records 以及涉及它们的 relation links 都会自动跳过。

```bash
# Exclude one type — Yarn
yarn strapi export --exclude-content-types api::article.article

# Exclude one type — NPM
npm run strapi export -- --exclude-content-types api::article.article

# Only specific types — Yarn
yarn strapi export --only-content-types api::article.article,api::category.category

# Only specific types — NPM
npm run strapi export -- --only-content-types api::article.article,api::category.category
```

### Exclude the entire media library

**Original:** Pass `media-library` to `--exclude` to exclude both upload binaries and upload content-type records. This is equivalent to combining `--exclude files` with `--exclude-content-types plugin::upload.file,plugin::upload.folder`.

**中文译文:** 向 `--exclude` 传入 `media-library` 可以同时排除 upload binaries 与 upload content-type records。它等价于组合使用 `--exclude files` 与 `--exclude-content-types plugin::upload.file,plugin::upload.folder`。

```bash
# Yarn
yarn strapi export --no-encrypt --exclude media-library

# NPM
npm run strapi export -- --no-encrypt --exclude media-library
```
