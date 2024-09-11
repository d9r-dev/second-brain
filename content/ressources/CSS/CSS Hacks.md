---
title: CSS Hacks
draft: false
publish: true
tags:
  - 🌲
date: 2024-09-04
---
## Expand the background of a container with less than 100% vw over the whole viewport

Give the container following CSS rule:

```CSS
.example {
	box-shadow: 0 0 0 100vmax #ccc;
	clip-path: inset(0 -100vmax);
}
```