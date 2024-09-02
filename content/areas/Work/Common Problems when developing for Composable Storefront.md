---
title: Common Problems when developing for Composable Storefront
draft: false
publish: false
tags:
  - composable-storefront
  - SAP-Commerce
date: 2024-09-02
---
* If you set up your storefront url to https, you need to make sure that the development server is run in ssl mode:
```
yarn start --ssl
```

* if chrome is telling you that you cannnot acces the localhost site because the cerficate is not truested:
	* set the following flag in `chrome:://flags`
	* ![a4689a6fc070d3cc7af2115c2bf08040.png](a4689a6fc070d3cc7af2115c2bf08040.png)
* You get the webpack watchpack Error: ``Error: ENOSPC: System limit for number of file watchers reached,...``, you can bump up the number of watchers in ubuntu with ``echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p``
* To run tests in composable storefront repo you need to set your CHROME_BIN variable to your local chrome installation, for example:
	* ![3821394d47d3a7294f68ca0d49b734ec.png](3821394d47d3a7294f68ca0d49b734ec.png)