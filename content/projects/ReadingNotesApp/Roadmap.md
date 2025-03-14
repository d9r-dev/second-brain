---
title: Roadmap
draft: false
publish: true
tags:
  - 📬
date: 2025-03-14
---
# Roadmap: Browser-Tabs-Synchronisation & Reader Mode Anwendung

Diese Roadmap bietet eine detaillierte Schritt-für-Schritt-Anleitung mit abhakbaren ToDos zur Entwicklung der Anwendung. Neben den einzelnen Implementierungsschritten findest du auch offene Fragen, die noch geklärt werden müssen.

---

## 1. Projekt Setup und Tauri Grundlagen

- [ ] **Rust und Tauri Installation**
  - [ ] Rust-Toolchain installieren (falls noch nicht vorhanden)
  - [ ] Node.js und npm/yarn installieren
  - [ ] Tauri CLI und Abhängigkeiten installieren
- [ ] **Initialisierung des Tauri-Projekts**
  - [ ] Neues Tauri-Projekt mit gewünschtem Frontend-Framework (z. B. React, Vue, Svelte oder plain HTML/JS/CSS) anlegen
  - [ ] Grundlegende Projektstruktur überprüfen
- [ ] **Dokumentation & Lernziele**
  - [ ] Tauri Architektur und Sicherheitskonzepte verstehen
  - [ ] Rust-Grundlagen (asynchrones Programmieren, Fehlerbehandlung) auffrischen

---

## 2. Browser-Tabs-Akquisition

- [ ] **Ansatz festlegen**
  - [ ] Recherche zu Browser-Erweiterungen zur Tab-Akquisition
  - [ ] Abwägen: Browser-Erweiterung vs. manuelle Eingabe der URLs
- [ ] **Browser-Erweiterung (falls gewünscht)**
  - [ ] Erste Version der Erweiterung entwickeln, um offene Tabs auszulesen
  - [ ] Kommunikationsschnittstelle zwischen Erweiterung und Tauri-App definieren (z. B. WebSocket, lokaler Server, benutzerdefiniertes Protokoll)
  - [ ] Sicherheits- und Datenschutzaspekte prüfen und implementieren
- [ ] **Fallback: Manuelle URL-Eingabe**
  - [ ] Benutzeroberfläche zum Einfügen/Importieren von URLs erstellen
- [ ] **Offene Fragen**
  - Wie soll die sichere Kommunikation zwischen der Browser-Erweiterung und der Tauri-App realisiert werden?
  - Welches Protokoll (z. B. WebSocket vs. HTTP-Endpunkt) ist am besten geeignet?

---

## 3. Fetching Web Pages

- [ ] **HTTP-Anfragen implementieren**
  - [ ] Rust Crate `reqwest` (oder Alternative) für asynchrone HTTP-Anfragen einbinden
  - [ ] Funktion zur Verarbeitung von HTTP-Fehlern und Timeouts implementieren
- [ ] **Caching und Wiederholte Zugriffe**
  - [ ] (Optional) Caching-Mechanismen einbauen, um wiederholte Downloads zu vermeiden
- [ ] **Testfälle schreiben**
  - [ ] Unit-Tests für HTTP-Anfragen und Fehlerfälle erstellen

---

## 4. HTML in „Reader Mode“ umwandeln

- [ ] **Recherche zu bestehenden Bibliotheken**
  - [ ] Überprüfen, ob es Rust Crates oder JavaScript-Bibliotheken gibt, die einen „Readability“-Algorithmus bereitstellen
- [ ] **Implementierung der HTML-Extraktion**
  - [ ] Mit Rust Crates wie `scraper` oder `select` die Hauptinhalte (Artikel/Body) extrahieren
  - [ ] Logik zur Entfernung von unnötigen Inhalten (Werbung, Navigation etc.) implementieren
- [ ] **Frontend-Darstellung**
  - [ ] CSS-Styles für eine leserfreundliche Darstellung entwickeln
- [ ] **Offene Fragen**
  - Soll eine bestehende JavaScript-Lösung (z. B. Mozilla Readability) integriert werden oder eine reine Rust-Lösung entwickelt werden?

---

## 5. UI für Text-Hervorhebung und Annotation

- [ ] **Reader Mode Anzeige**
  - [ ] Implementierung der Ansicht für den bereinigten Content
- [ ] **Text-Hervorhebungsfunktion**
  - [ ] Integration einer JavaScript-Bibliothek (z. B. Rangy oder alternative) zur Textauswahl und Hervorhebung
  - [ ] Logik zum Erfassen der hervorgehobenen Textpassagen und deren Position bzw. Kontext entwickeln
- [ ] **Markdown Editor**
  - [ ] Editor-Komponente für Markdown-Notizen einbinden (kann z. B. ein einfaches Textarea sein oder ein fortgeschrittener Editor)
  - [ ] Möglichkeit implementieren, hervorgehobene Textstellen als Zitate in den Editor einzufügen
- [ ] **Metadaten speichern**
  - [ ] Verknüpfung der Hervorhebungen mit Original-URLs und ggf. Positionen implementieren

---

## 6. Export der Daten in Markdown

- [ ] **Markdown Formatierung definieren**
  - [ ] Struktur (z. B. Blockzitate für Markierungen, Listen oder Inline-Kommentare für Notizen) festlegen
- [ ] **Dateisystem-Integration**
  - [ ] Nutzung von Tauri’s API oder Rust File I/O zur sicheren Dateierstellung implementieren
  - [ ] Dialog zur Dateispeicherort- und Namensauswahl für den Benutzer integrieren
- [ ] **Testen der Exportfunktion**
  - [ ] Exportierte Dateien in verschiedenen Szenarien überprüfen (z. B. leer, mit mehreren Notizen/Hervorhebungen)

---

## 7. Testen, Debuggen und Deployment

- [ ] **Testen**
  - [ ] Unit-Tests für die Rust-Komponenten (HTTP-Fetching, HTML-Parsing) schreiben und ausführen
  - [ ] Integrationstests für die UI (Hervorhebung, Notizen-Erfassung) durchführen
- [ ] **Debugging**
  - [ ] Sicherstellen, dass die Kommunikation zwischen Rust-Backend und JavaScript-Frontend reibungslos funktioniert
  - [ ] Plattformübergreifende Unterschiede (Windows, macOS, Linux) berücksichtigen und testen
- [ ] **Deployment**
  - [ ] Tauri-spezifische Packaging-Tools verwenden, um die Anwendung für verschiedene Betriebssysteme zu paketieren
  - [ ] Deployment-Dokumentation erstellen

---

## 8. Dokumentation und abschließende Überprüfung

- [ ] **Nutzer-Dokumentation**
  - [ ] Anleitung zur Bedienung der Anwendung (Synchronisation, Hervorhebung, Notizen, Export) erstellen
- [ ] **Entwickler-Dokumentation**
  - [ ] Code-Dokumentation und Architekturübersicht verfassen
  - [ ] Offene Fragen und getroffene Entscheidungen dokumentieren
- [ ] **Code-Review und Refactoring**
  - [ ] Feedback von Testnutzern einholen und notwendige Anpassungen umsetzen
- [ ] **Offene Fragen zusammenfassen**
  - Wie wird die Erweiterung zukünftig aktualisiert und gepflegt?
  - Welche Sicherheitsmaßnahmen müssen zusätzlich implementiert werden, um die Kommunikation zwischen Browser-Erweiterung und Tauri-App zu sichern?

---

## Abschluss

Diese Roadmap soll als lebendiges Dokument dienen. Neue Erkenntnisse und Änderungen im Projektverlauf sollten hier ergänzt werden. Arbeite die Aufgaben Schritt für Schritt ab und passe die Planung an, wenn sich Anforderungen ändern oder neue Herausforderungen auftreten.
