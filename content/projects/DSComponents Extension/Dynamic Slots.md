---
title: Dynamic Slots
draft: false
publish: false
tags:
  - SAP-Commerce
  - 🌱
date: 2024-09-02
---
- Smaredit komponente
	- Sicherstellen, dass Komponente nur angezeigt wird, wenn dynamisches template verwnedet wirddynam
- Template mit ~20 Slotnames
	- JSP anlegen
	- Layout in Composable Storefront registrieren?
	- Impex
	
- Bei klick auf Button --> Slot und ContentSlotRelationForPage wird erzeugt
- Contentslot erweitern mit größe und dann beim Rendern einfach die Klasse für die Breite setzen
- eigenes Tag schreiben, dass die breite dann an einen Container für die Slots renderd

- Wenn man eine Page im Smartedit anlegt, dann werden automatisch Contentslots für alle ConetntSlotNames angelegt
	- das muss verhindert werden
	- Klasse überschreiben?
	- Erstellen von Seite führt POST an /cmsitem Endpunkt aus CMSItemController.java
	- DefaultPageInitializer erstellt Content-Slots
	- Klasse überschrieben mit CustomPageInitializier
- erstellen von Contentslot
	- active: Boolean true
	- cataogVersion
	- item blockedfor sync boolea false
	- ID: String --> page_slot_size
- ContentSlot For Page
	- ContentSlot
	- Page
	- Position --> String
	- CatalogVersion
	- ID: String --> page_slot_position
- DefaultCMSAdminContentSlotServic verwenden um Slot und Relation zu erstellen
- CMSItemController erweitern oder eigenen controller anlegen?
	- Anfrage an endpunkt mit Liste von CotentSlotIds und Größe