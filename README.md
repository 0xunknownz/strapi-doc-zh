# strapi-doc-zh

Strapi 官方文档的中英文对照翻译项目。

- 上游仓库：`strapi/documentation`
- 上游目录：`docusaurus/docs`
- 历史计数基准：`6a71f594f4023fee59d5877757874601b0e45f35`，353 个文件（沿用此前登记，未在本批重新盘点）。
- 本批源文版本：`d3cbe0c728c53920d40e3963c0a57cca0d68dbeb`。

## 进度

累计登记覆盖：**208/353**，即此前登记的 206 个文件，加上本批新增的 2 个文件。

> 登记覆盖数不等于逐段全文校验合格数。本批没有对全部历史译文重新审校；各文件的实际来源以其自身标注的源文件 SHA 或批次记录为准，不能将所有文件视为同一上游快照。

## 本批全文对照

| 文档 | 正文对照组数 | 原样保留的代码块 |
|---|---:|---:|
| [使用 Entity Service API 筛选数据](docs/cms/api/entity-service/filter.md) | 60 | 26 |
| [Documentation 插件](docs/cms/plugins/documentation.md) | 47 | 8 |

本批已核对源文件 Git blob SHA、正文与表格覆盖、代码块一致性及中英文间距。共处理 155 个文本单元（含标题、提示和元数据描述），形成 107 组正文对照，保留 34 个原文代码块。MDX 展示组件已转换为 GitHub 可读形式；交互演示保留上游入口。此处的检查不包含运行示例或验证插件兼容性。

详见 [本批校验记录](translation-batches/2026-09-23-entity-service-documentation.json) 和 [翻译进度](STATUS.md)。

## 此前已登记的模块

包括 Cloud、Query Engine API、后端自定义、TypeScript、部署指南，以及 Plugin Server API、Admin Panel API 和插件开发指南。历史登记保留，但不据此宣称全部内容已通过全文完整性审校。

## 规范与来源

译文遵循 [术语表](GLOSSARY.md) 和 [翻译规范](TRANSLATION_GUIDE.md)。上游原文版权及许可声明见 [UPSTREAM_LICENSE](UPSTREAM_LICENSE)。
