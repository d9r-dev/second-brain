---
title: Patterns for Memory Efficient DOM Manipulation
draft: false
publish: true
tags:
  - javascript
  - html
  - web-dev
date: 2024-09-02
---
[Patterns for Memory Efficient DOM Manipulation](https://frontendmasters.com/blog/patterns-for-memory-efficient-dom-manipulation/)

- use vanilla [[Javascript]]
- prefer hiding over creating DOM elements
- Prefer textContent over innerText for reading the content of an element
- Use insertAdjacentHTML over innerHTML
- use insertAdjacentElement or appendChild
	- use the template tag to create HTML remplates and appendChild to insert new HTML
	- use createDocumentFragment with appendChild to Batch Inserts
- Use AbortController to unbind groups of events