---
title: Turn of DB_AUDIT logs in local development environemnt
draft: false
publish: true
tags:
  - 🌲
  - SAP-Commerce
  - tricks
date: 2024-11-05
---
SAP Commerce's database audit logging can get really annoying. Every database interaction creates a `DB_AUDIT` log from the `AuditbaleActionsHandler`. Especially, if you want to debug a database heavy class it can get really hard to find your beloved debug logs in between all the audit logs. But turning off the audit logs isn't that easy. 

I found [this article about audit logging](https://community.sap.com/t5/crm-and-cx-blogs-by-members/audit-data-and-audit-logging-in-sap-commerce/ba-p/13738362). It suggests to set the following properties: 
```
log4j2.logger.auditableActionsHandler.name=de.hybris.platform.audit.actions.impl.Slf4jAuditableActionHandler
log4j2.logger.auditableActionsHandler.level=OFF
``` 
That did not work for me. Even after setting the properties in the properties in my `local.properties` I got all the logs. Also editing the Log4J config did not work. Then I found [this note](https://me.sap.com/notes/3342126/E) from SAP. The only thing that seems to work is to turn off the logging for every item type. But how do you know which types to set? Here is an easy step by step solution.

1. You need to install xmlstarlet
```bash
sudo apt install xmlstarlet
```
2. Go to your source
```bash
cd path/to/hybris/bin  
```
3. Find all item types that are enabled for database audit logging.
```bash
find . -name "*-items.xml" | xargs xmlstarlet select -t -m "//itemtype" -n -v "concat(concat('dbaudit.', @code), '.disabled=true')" | sort | uniq > dbaudit.txt
```

You will get a text file `dbaudit.txt` with all item types and the `dbaudit.<itemtype>.disbaled` property set to true. Now, turn everything into lower case,  and put them into your `local.properties`. Voila! The logging is gone.

Blog Post: https://community.sap.com/t5/crm-and-cx-blogs-by-members/audit-data-and-audit-logging-in-sap-commerce/ba-p/13738362

SAP Help: https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/aa417173fe4a4ba5a473c93eb730a417/3a3ba7e718324544964710f297b47661.html