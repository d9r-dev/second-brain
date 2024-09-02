---
title: Modify Nested Editors in backoffice-config
draft: false
publish: true
tags:
  - SAP-Commerce
  - Backoffice
date: 2024-09-02
---
I created a new Type for localized maps and the backoffice does not know OOTB how to handle that. So I wanted just the usual Backoffice editor for maps but nested in the localized editor. There is actually an article in the SAP Commerce documentation: [SAP Help Nested Editors](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/9b5366ff6eb34df5be29881ff55f97d2/8c163f19866910148f748048c64841eb.html?locale=en-US)

Here are some extra things to consider:

- Make sure your backoffice-config.xml follows the following name convention: `<my-extension-name>-backoffice-config.xml` and is located in the resources directory of your extension
- Your file must be a valid XML so do not forget the `<config>` and `<?xml>` tag
- If your extension is no backoffice extension then you need to add `<meta key="backoffice-module" value="true" />` to your extensionfino.xml
- It is pretty confusing that in the help article 3 lines per attribute are shown in the example. You actually only need one line per attribute. 
- For me it was not possible to just change the editor for the fields in the unbound section. The only thing that worked for me was to add the fields to another section and then change the editor.

Example:

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<config xmlns="http://www.hybris.com/cockpit/config">
    <context merge-by="type" parent="SimpleCMSComponent" type="DSComposableComponent" component="editor-area" module="dscomponents">
    <editorArea:editorArea xmlns:editorArea="http://www.hybris.com/cockpitng/component/editorArea">
        <editorArea:tab name="hmc.properties">
            <editorArea:section name="hmc.essential">
                <editorArea:attribute editor="com.hybris.cockpitng.editor.localized(com.hybris.cockpitng.editor.defaultmap)" qualifier="dynamicFields"/>
                <editorArea:attribute qualifier="htmlMarkup" />
            </editorArea:section>
        </editorArea:tab>
    </editorArea:editorArea>
</context>
</config>
```

 