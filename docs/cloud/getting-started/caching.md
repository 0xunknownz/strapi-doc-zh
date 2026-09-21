# 📖 对照翻译：Cloud caching & performance

> Source: `docusaurus/docs/cloud/getting-started/caching.md`  
> Upstream SHA: `29a4fe653946ad425c74e506778328cf65bb3881`

**Original:** Cloud caching & performance

**中文译文:** Cloud 缓存与性能

**Original:** Edge caching via Cache-Control headers reduces latency and server load for heavy static content.

**中文译文:** 对体积较大的静态内容，通过 `Cache-Control` header 启用边缘缓存，可以降低延迟并减轻服务器负载。

**Original:** For Strapi Cloud applications with large amounts of cacheable content, such as images, videos, and other static assets, enabling CDN (Content Delivery Network) caching via the `Cache-Control` header can help improve application performance.

**中文译文:** 对于包含大量可缓存内容的 Strapi Cloud 应用，例如图片、视频和其他静态资源，可以通过 `Cache-Control` header 启用 CDN（Content Delivery Network）缓存，从而提升应用性能。

**Original:** CDN caching can help improve application performance in a few ways:

* **Reducing Latency**: Caching frequently accessed content on edge servers located closer to the end-users can reduce the time it takes to load content.
* **Offloading Origin Server**: By caching content on edge servers it can offload the origin server, reducing the load and allowing it to focus on delivering more dynamic content.
* **Handling Traffic Spikes**: Help handle traffic spikes by distributing the load across multiple edge servers. This can prevent the origin server from becoming overwhelmed during peak traffic times and ensures a consistent user experience.

**中文译文:** CDN 缓存可以通过以下几种方式提升应用性能：

* **降低延迟**：将高频访问的内容缓存到距离终端用户更近的 edge server，可以缩短内容加载时间。
* **减轻 origin server 负载**：把内容缓存到 edge server 后，可以分担 origin server 的请求压力，让它更专注于动态内容的处理与交付。
* **应对流量峰值**：通过多个 edge server 分摊负载，有助于处理突发流量，避免 origin server 在高峰期过载，从而保持一致的用户体验。

## Cache-Control Header in Strapi Cloud

**Original:** Static sites deployed on Strapi Cloud include, by default, a `Cache-Control` header set to cache for 24 hours on CDN edge servers and 10 seconds in web browsers. This is done to ensure that the latest version of the site is always served to users.

**中文译文:** 部署在 Strapi Cloud 上的静态站点默认包含 `Cache-Control` header：在 CDN edge server 上缓存 24 小时，在 Web 浏览器中缓存 10 秒。这样的设置旨在兼顾缓存收益，同时确保用户能够及时获取站点的最新版本。

**Original:** Responses from dynamic apps served by Strapi Cloud are not cached by default. To enable caching, you must set the `Cache-Control` header in the app’s `HTTP` response functions.

**中文译文:** Strapi Cloud 提供服务的动态应用，其响应默认不会被缓存。若要启用缓存，需要在应用的 `HTTP` 响应函数中设置 `Cache-Control` header。

**Original code (kept unchanged):**

```js
function myHandler(req, res) {
  // Set the Cache-Control header to cache responses for 1 day
  res.setHeader('Cache-Control', 'max-age=86400');
  
  // Add your logic to generate the response here
}
```

**中文译文:** 上面的 JavaScript 示例通过 `res.setHeader('Cache-Control', 'max-age=86400')` 将响应缓存时间设置为 1 天。代码保持原样。

**Original code (kept unchanged):**

```ts
import { Request, Response } from 'express';

function myHandler(req: Request, res: Response) {
  // Set the Cache-Control header to cache responses for 1 day
  res.setHeader('Cache-Control', 'max-age=86400');
  
  // Add your logic to generate the response here
}
```

**中文译文:** 上面的 TypeScript 示例作用相同：在响应中设置 `Cache-Control: max-age=86400`，让响应缓存 1 天。代码保持原样。
