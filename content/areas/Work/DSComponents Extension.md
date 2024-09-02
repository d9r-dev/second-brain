---
title: DSComponents Extension
draft: false
publish: false
tags:
  - SAP-Commerce
  - Extension
date: 2024-09-02
---
# DSComponents
## Extensions Modules
* **DSComponents**: contains the basic code for the features and components
* **DSSmartedit**: extends Smartedit to allow editing the new components
* **DSComponentsstorefrontaddon**: Addon for Accelerator Storefronts
* **ComposableStorefront Components**: Angular components for the Composable Storefront 


## Installing the extensions
### DSComponents
1. Add the extension to your localextensions.xml
```
<extensions name='dscomponents' />
```
2. Import all Impexes from the ressources directory
3. Trigger a "Update running system" from the HAC

### DSSmartedit
1. Add the extension to your localextensions.xml
```
<extensions name='dssmartedit' />
```
2. Rebuild the system and start the server

### DScomponentsstorefrontaddon for Accelerator Storefront
1.  Extension zu localextensions.xml hinzufügen
```
<extension name='dscomponentsstorefrontaddon' />
```
2. Be sure your localextensions.xml also contains 'addonsupport' extension

3. In the platform directory run:
```
ant addoninstall -Daddonnames="dscomponentsstorefrontaddon" -DaddonStorefront.yacceleratorstorefront="<name-of-the-storefront>"
```
4. Rebuild the system and start the server

### Components for Composable Storefront
1. Copy the dscomponents directory into the src/app directory
![192c952287eae835637e0209b6583a65.png](192c952287eae835637e0209b6583a65.png)
2. Import the `DSComposableComponentModule` into your `AppModule`
![2931996e1f57d7f8c72405c0b7fa9b83.png](2931996e1f57d7f8c72405c0b7fa9b83.png)
4. Build and run the storefront

## Components
### DSComposableComponent

A component that allows content maintainers to create small components in a flexible way. You can create a HTML template and mark parts of it with {{<key>}}. All so marked keys, get turned into fields that are editable in the smartedit Editor. The values maintained in the field are then getting interpolated back into the template when rendering the component. The component is usable in accelerator and composable storefronts.

![1dd6614d9a23045bcaa401b74a241319.png](1dd6614d9a23045bcaa401b74a241319.png)
![24f05a1c0601a9c1a0927899563bd8e8.png](24f05a1c0601a9c1a0927899563bd8e8.png)

**HTML Template**: Contains the Template that is getting renderd. Words sorrounded by {{}}  will become keys for dynamic fields when saving the component once.
**Dynamic Fields**: Fields that got extrapolated from the HTML Template. The values will be rendered in the component when displaying the component in the storefront.