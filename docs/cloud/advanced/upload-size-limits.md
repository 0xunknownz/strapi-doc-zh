# 📖 对照翻译：Upload size limits for Strapi Cloud

> Source: `docusaurus/docs/cloud/advanced/upload-size-limits.md`  
> Upstream SHA: `8953d31ad8e9935452bf3d440575497ee8e865bd`

**Original:** Upload size limits for Strapi Cloud

**中文译文:** Strapi Cloud 上传大小限制

**Original:** Non-image files are capped at 200 MB on all plans. Image files have a memory-based recommended maximum that varies by format, plan, and Media Library settings. To upload larger images, disable Responsive friendly upload and Size optimization.

**中文译文:** 所有方案的非图片文件上传上限均为 200 MB。图片文件则采用基于内存的建议最大值，该值会随图片格式、方案以及 Media Library 设置而变化。如果需要上传更大的图片，请关闭 Responsive friendly upload 和 Size optimization。

**Original:** Strapi Cloud applies 2 distinct limits to uploads. The first is a hard maximum file size, enforced at the infrastructure level for non-image files. The second is a memory-based recommendation for image files that depends on your CMS settings.

**中文译文:** Strapi Cloud 对上传应用 2 类不同限制。第一类是针对非图片文件的硬性最大文件大小，由基础设施层强制执行；第二类是针对图片文件、基于内存使用情况的建议上限，并会受到 CMS 设置影响。

## Maximum upload file size for non-image files

**Original:** Non-image uploads are capped at 200 MB on all Strapi Cloud plans. The cap is enforced at the infrastructure level and cannot be overridden via the `strapi::body` middleware configuration.

**中文译文:** 所有 Strapi Cloud 方案中，非图片文件的上传上限都是 200 MB。该限制由基础设施层强制执行，无法通过 `strapi::body` middleware 配置覆盖。

## Recommended maximum upload size for image files

**Original:** Image uploads are subject to an additional, memory-driven recommendation that is independent of the non-image cap and varies by image format.

**中文译文:** 图片上传还受到额外的、由内存消耗决定的建议限制。它独立于非图片文件的 200 MB 硬性上限，并且会根据图片格式变化。

**Original:** To upload an image larger than the recommended maximum, disable both Responsive friendly upload and Size optimization in the Media Library settings. The CMS then stores the source file as-is without in-process processing, which raises the recommended maximum.

**中文译文:** 若要上传超过建议上限的图片，请在 [Media Library settings](/cms/features/media-library#configuring-settings) 中同时关闭 Responsive friendly upload 和 Size optimization。这样 CMS 会直接按原样保存源文件，不再进行进程内处理，从而提高建议最大值；可参考下方 *Processing off* 表格。

**Original:** When Responsive friendly upload and Size optimization are both enabled in the Media Library settings, the CMS resizes the source image and generates a set of thumbnails (small, medium, large) in the instance's memory before persisting them. This processing happens in-process, regardless of the configured upload provider.

**中文译文:** 当 Media Library settings 中的 Responsive friendly upload 和 Size optimization 都启用时，CMS 会先在实例内存中缩放源图片，并生成一组 thumbnails（`small`、`medium`、`large`），然后再进行持久化。无论配置了什么 upload provider，这些处理都会在 Strapi Cloud 实例进程内执行。

**Original:** Switching to a third-party provider (Amazon S3, Cloudinary, etc.) is not a workaround. The resize and thumbnail generation step still runs inside the Strapi Cloud instance and still requires memory proportional to the source image dimensions.

**中文译文:** 切换到第三方 provider（例如 Amazon S3、Cloudinary）并不能绕过这一限制。图片 resize 与 thumbnail 生成仍然发生在 Strapi Cloud 实例内部，并且所需内存仍与源图片尺寸成比例。

**Original:** Actual memory usage depends on the image dimensions, format, and your Media Library settings. The values in the following tables are a recommendation, not a hard limit. Uploads above the recommended size are likely to cause the instance to run out of memory and restart.

**中文译文:** 实际内存使用量取决于图片尺寸、格式以及 Media Library 设置。下面表格中的数值是**建议值**，不是硬性限制。上传超过建议大小的图片，很可能导致实例内存耗尽并重启。

**Original:** The recommendation depends on whether Responsive friendly upload and Size optimization are enabled in the Media Library settings:

- _Processing on_: both settings enabled, with the default `small`, `medium`, and `large` sizes. Strapi generates the thumbnails in memory, so the safe upload size is lower.
- _Processing off_: both settings disabled. The source image is stored as-is with no in-process processing, so the safe upload size is higher.

**中文译文:** 建议最大值取决于 Media Library settings 中是否启用了 Responsive friendly upload 和 Size optimization：

- *Processing on*：两项设置都启用，并使用默认的 `small`、`medium` 和 `large` 尺寸。Strapi 会在内存中生成 thumbnails，因此安全上传大小更低；
- *Processing off*：两项设置都关闭。源图片按原样存储，不执行进程内处理，因此安全上传大小更高。

**Original:** Recommended maximum image size, expressed in megapixels (MP), per format and plan:

**中文译文:** 以下是不同图片格式和方案对应的建议最大图片尺寸，单位为 megapixels（MP）。

**Original — Processing on:**

| Format | Starter | Pro & Business |
|--------|------------------|-------------|
| JPEG   | 26 MP            | 135 MP      |
| PNG    | 10 MP            | 90 MP       |
| WebP   | 4 MP             | 12 MP       |
| TIFF   | 24 MP            | 125 MP      |
| AVIF   | 92 MP            | 92 MP       |

**中文译文 — Processing on:**

| 格式 | Starter | Pro & Business |
|--------|------------------|-------------|
| JPEG   | 26 MP            | 135 MP      |
| PNG    | 10 MP            | 90 MP       |
| WebP   | 4 MP             | 12 MP       |
| TIFF   | 24 MP            | 125 MP      |
| AVIF   | 92 MP            | 92 MP       |

**Original — Processing off:**

| Format | Starter | Pro & Business |
|--------|------------------|-------------|
| JPEG   | 224 MP           | 265 MP      |
| PNG    | 24 MP            | 115 MP      |
| WebP   | 15 MP            | 40 MP       |
| TIFF   | 24 MP            | 125 MP      |
| AVIF   | 96 MP            | 96 MP       |

**中文译文 — Processing off:**

| 格式 | Starter | Pro & Business |
|--------|------------------|-------------|
| JPEG   | 224 MP           | 265 MP      |
| PNG    | 24 MP            | 115 MP      |
| WebP   | 15 MP            | 40 MP       |
| TIFF   | 24 MP            | 125 MP      |
| AVIF   | 96 MP            | 96 MP       |

**Original:** The number of megapixels of an image is its width multiplied by its height in pixels, divided by 1,000,000. The pixel dimensions that match a given megapixel count depend on the aspect ratio. For a square image, 1 MP is roughly 1000×1000 px, 4 MP is roughly 2000×2000 px, and 100 MP is roughly 10000×10000 px.

**中文译文:** 图片的 megapixels 计算方式为：像素宽度 × 像素高度 ÷ 1,000,000。给定 MP 对应的实际像素尺寸取决于 aspect ratio。对于正方形图片，1 MP 大约对应 1000×1000 px，4 MP 大约对应 2000×2000 px，100 MP 大约对应 10000×10000 px。

**Original:** To configure external storage such as Amazon S3 or Cloudinary, see Upload Provider Configuration for Strapi Cloud.

**中文译文:** 如果要配置 Amazon S3、Cloudinary 等外部存储，请参阅 [Upload Provider Configuration for Strapi Cloud](/cloud/advanced/upload)。
