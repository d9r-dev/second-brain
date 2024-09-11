---
title: Intercepting Populated Item Models Before Persistence
draft: false
publish: true
tags:
  - SAP-Commerce
  - 🌲
date: 2024-09-02
---
Let’s say you have written a new CMS Component and want to intercept the populated item model before persisting it to the database to make some transformations on its data. There is a pretty straightforward explanation on how to do this on the SAP Help [Extending the CMS Item API](https://help.sap.com/docs/SAP_COMMERCE/9d346683b0084da2938be8a285c0c27a/cf0445b16a4f44d9844381a34572d7b8.html)

Under "Configuring the New Populator" the explanation gets a bit confusing. So here is how it actually works:

After you created your populator, you create the bean for it:
```
<bean id="customItemContentPopulator" class="path.to.populator.CustomItemContentPopulator"/>
```

Then the article says the following:
> You must then map your Custom Item Type to the new populator to make it visible to the CMS Item Type Populator Provider. The following code shows the configuration for the new populator:
> ```XML
> <bean id="customItemContentPopulator" class="path.to.populator.CustomItemContentPopulator"/>
> 
> <bean depends-on="cmsContentItemTypePopulatorsMap" parent="mapMergeDirective">
> 		<property name="key" value="CustomItem"/>
> 		<property name="value" ref="customItemContentPopulator"/>
> </bean>
> ```

If you do this, only your populator will be called for the component. That means other populators, like the one that will handle the saving of the content slot where the component is contained, will not be called. Often that is, of course, not what we want. The documentation then states the following:

>If you want to apply many populators to the same CMS item type, you can use a composite populator to configure the new populator as follows:
>```XML
><bean id="cmsContentItemTypePopulatorsMap" parent="cmsCompositePopulator">
>  <property name="populators">
>      <list merge="true">
>        <bean id="customItemContentPopulator" class="path.to.populator.CustomItemContentPopulator"/>
>      </list>
>   </property>
></bean> 
>```

That is fine as far as it goes, but of course you have to add the other populators as well, or you will only have one populator in your map again. Also, you have to add your populators map to the `cmsContentItemTypePopulatorsMap`. So your config should look something like this:

```XML
<alias name="dsCustomComponentContentPopulator" alias="defaultCustomComponentContentPopulator"/>
    <bean id="customComponentContentPopulator" class="de.custom.components.populators.CustomComponentContentPopulator" />

    <bean id="cmsCustomComponentItemTypePopulatorsMap" parent="cmsCompositePopulator">
        <property name="populators">
            <list merge="true">
                <ref bean="defaultCustomComponentContentPopulator"/>
                <bean class="de.hybris.platform.cmsfacades.cmsitems.populators.AbstractCMSComponentContentPopulator">
                    <property name="contentSlotAdminService" ref="cmsAdminContentSlotService"/>
                    <property name="uniqueItemIdentifierService" ref="cmsUniqueItemIdentifierService"/>
                    <property name="validationDtoFactory" ref="validationDtoFactory"/>
                    <property name="componentTypeAllowedForContentSlotPredicate" ref="componentTypeAllowedForContentSlotPredicate"/>
                    <property name="relationBetweenComponentsService" ref="relationBetweenComponentsService"/>
                </bean>
                <bean class="de.hybris.platform.cmsfacades.cmsitems.populators.CMSItemLinkToggleDataToModelPopulator">
                    <property name="cmsModelContainsLinkTogglePredicate" ref="cmsModelContainsLinkTogglePredicate"/>
                </bean>
            </list>
        </property>
    </bean>

    <bean depends-on="cmsContentItemTypePopulatorsMap" parent="mapMergeDirective">
        <property name="key" value="CustomComponent"/>
        <property name="value" ref="customComponentItemTypePopulatorsMap"/>
    </bean>
```

