---
title: Using Playwright to Test in WebKit Browser (Safari)
draft: false
publish: true
tags:
  - 🌲
  - E2E-testing
  - testing
  - playwright
date: 2025-03-14
---
## Tutorial

### Prerequisites 

You need to have installed Node.js and npm.
### Steps

1. Open up your terminal/powershell and type `npx playwright install`.
2. To open a URL in WebKit run  the following command `npx playwright wk <your-url>`

What you get is a WebKit Browser with your URL opened. You can even use the WebKit Inspector. Depending on your operating system not all features will be identical to the branded version of Safari. For that you should use MacOS. But still you can see how WebKit is rendering your site and identify some problems that may occur, without opening Browserstack or using an actually Apple device.

The Playwright [documentation](https://playwright.dev/docs/browsers#open-pages) states the following:

> Playwright's WebKit is derived from the latest WebKit main branch sources, often before these updates are incorporated into Apple Safari and other WebKit-based browsers. This gives a lot of lead time to react on the potential browser update issues. Playwright doesn't work with the branded version of Safari since it relies on patches. Instead, you can test using the most recent WebKit build.
>
> Note that availability of certain features, which depend heavily on the underlying platform, may vary between operating systems. For example, available media codecs vary substantially between Linux, macOS and Windows. While running WebKit on Linux CI is usually the most affordable option, for the closest-to-Safari experience you should run WebKit on mac, for example if you do video playback.