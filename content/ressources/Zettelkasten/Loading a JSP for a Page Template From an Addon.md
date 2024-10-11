---
title: Loading a frontend template for a CMS Page from an addon
draft: false
publish: true
tags:
  - 🌲
  - SAP-Commerce
  - smart-edit
date: 2024-10-11
---
If you use an Accelerator Storefront in your SAP Commerce project, you might want to introduce a new page template for a CMS site. A page template needs an associated JSP that is used to render the page. You add the path to the JSP in the field `frontendTemplateName`. So, we could write an Impex like this:

```Impex
INSERT_UPDATE PageTemplate; $contentCV[unique = true]; uid[unique = true]; name; frontendTemplateName; restrictedPageTypes(code); active[default = true];  
                          ;                          ; <YourPageTemplate>; <YourPageTemplateName>; /pages/layout/<your-template>; ContentPage;
```

If we do it like this, the template is loaded from your storefront extension in the following directory: `<yourstorefrontextension>/web/webroot/WEB-INF/views/responsive/pages/layout`.

Now, I created a[ storefront addon extension to modify an existing storefront](https://help.sap.com/docs/SAP_COMMERCE/b490bb4e85bc42a7aa09d513d0bcb18e/8adf7365866910149ceb975f778d809d.html). JSPs from an addon get copied into the storefront in the `views/addons/<youraddon>/responsive/`. So, how do we tell the system to look into that directory? It does not work to just write something like `../addons/<youraddon>/responsive/pages/layout`. 

It took me some time and extensive Google searches to find the solution: The string in the `frontendTemplateName` gets special parsing treatment. The storefront has a `UiExperienceViewResolver`, and there the path to the template gets parsed. As it turns out, if you put `addon:` before your path, SAP Commerce searches in the addon directory instead of the base storefront template directory. So, if we change the string for the `frontendTemplateName` in the Impex to `addon:/<youraddon>/pages/layout/<your-template>`, it works just fine.

