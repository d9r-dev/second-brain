---
title: PRPL-Pattern
draft: false
publish: true
tags:
  - performance
date: 2024-09-02
---
- [Guide](https://web.dev/articles/apply-instant-loading-with-prpl)
- **Preload** the late discovered ressources
	- preload is a declarative fetch request that tells the browser to request a ressource that is otherwise not discoverable by the browser like images in background css code
	- Preload late-discovered resources by adding a `<link>` tag with `rel="preload"` to the head of your HTML document
	- Adding a `<link rel="preload">` directive will initiate a request for that resource and store it in the cache. The browser is then able to retrieve it when needed.
- **Render** the initial route as soon as possible
	- To improve First Paint, Lighthouse recommends inlining critical JavaScript and deferring the rest using [`async`](https://web.dev/articles/critical-rendering-path/adding-interactivity-with-javascript), as well as inlining critical CSS used above-the-fold. This improves performance by eliminating round-trips to the server to fetch render-blocking assets. However, inline code is harder to maintain from a development perspective and cannot be cached separately by the browser.
	-
- **Pre-Cache** remaining assets
	- By acting as a proxy, **service workers** can fetch assets directly from the cache rather than the server on repeat visits. This not only allows users to use your application when they are offline, but also results in faster page load times on repeat visits.
- **Lazy load** other routes and none-critical assets

References: [[Performance]] [[Frontend Development]]