# Detaillierter Implementierungsplan

Dieser Plan beschreibt, wie Du mit Go und Wails eine Anwendung realisieren kannst, die Browser-Tabs synchronisiert, Webseiten im vereinfachten Lesemodus anzeigt, einen integrierten Markdown-Editor bereitstellt und Zitate aus der Anzeige in Notizen einfügt sowie den Export der Notizen ermöglicht.

---

## 1. Projekt-Setup

- **Repository und Initialisierung:**  
  - Erstelle ein Git-Repository und initialisiere ein neues Wails-Projekt mit dem Befehl `wails init`.
  - Struktur: Trenne Backend (Go) und Frontend (HTML/JS/CSS).  
- **Werkzeuge & Abhängigkeiten:**  
  - Go (aktuelle Version)  
  - [Wails CLI](https://wails.io/)  
  - Für den Frontend-Bereich kannst Du ein Framework wie React, Vue oder Svelte wählen – Wails unterstützt alle.

---

## 2. Browser-Tabs Synchronisation

- **Browser-Integration:**  
  - **Browser-Erweiterung:**  
    - Entwickle eine kleine Erweiterung (z. B. für Chrome/Firefox) mit JavaScript, um die aktiven Tabs mittels der Browser-API (`chrome.tabs.query` bzw. `browser.tabs.query`) auszulesen.
    - Die Erweiterung sammelt URLs, Titel und eventuell weitere Metadaten.
  - **Kommunikation mit der App:**  
    - Sende die Tab-Daten an die App. Möglichkeiten:
      - **WebSocket:** Implementiere in Go einen lokalen WebSocket-Server mithilfe von [github.com/gorilla/websocket](https://github.com/gorilla/websocket), um Echtzeit-Kommunikation zu ermöglichen.
      - **HTTP-Endpoint:** Alternativ kann ein lokaler HTTP-Server in der App eingebunden werden, um Daten via REST zu empfangen.

---

## 3. Download und Verarbeitung von Webseiten

- **Seiten-Download:**  
  - Verwende Go’s Standardpaket `net/http` zum Herunterladen der Seiteninhalte.
- **Extraktion des Hauptinhalts:**  
  - Nutze [github.com/go-shiori/go-readability](https://github.com/go-shiori/go-readability) zur Implementierung des "Readability"-Algorithmus, um den Hauptinhalt aus HTML-Dokumenten zu extrahieren.
  - Optional: Weitere Verarbeitung mit [github.com/PuerkitoBio/goquery](https://github.com/PuerkitoBio/goquery) für zusätzliche Anpassungen.
- **Fehlerbehandlung:**  
  - Implementiere robustes Error-Handling für HTTP-Fehler, ungültige Inhalte oder Parsing-Fehler.

---

## 4. Anzeige im vereinfachten Lesemodus

- **Frontend-Komponente:**  
  - Entwickle eine Komponente im Frontend, die den extrahierten Inhalt (als HTML) anzeigt.
  - Verwende CSS für ein angenehmes Leseerlebnis (z. B. angepasste Schriftgrößen, Zeilenabstände und Farben).
- **Datenübertragung:**  
  - Übergebe den bereinigten HTML-Code vom Go-Backend an das Frontend über Wails-Methoden (z. B. direkte Funktionsaufrufe aus dem JavaScript).

---

## 5. Integration des Markdown-Editors

- **Editor-Auswahl:**  
  - Integriere einen bestehenden JavaScript-Markdown-Editor:
    - **Optionen:** [SimpleMDE](https://simplemde.com/), [Toast UI Editor](https://github.com/nhn/tui.editor) oder [CodeMirror](https://codemirror.net/) mit Markdown-Modus.
- **Konfiguration:**  
  - Konfiguriere den Editor hinsichtlich Syntax-Hervorhebung, Live-Preview (optional) und Anpassbarkeit.
  - Stelle sicher, dass der Editor nahtlos neben der Lesemodus-Anzeige platziert wird.

---

## 6. Text-Hervorhebung und Zitatfunktion

- **Implementierung der Selektion:**  
  - Füge in der Lesemodus-Komponente JavaScript-Event-Listener hinzu, die Textselektionen erkennen.
  - Bei einer Auswahl wird ein Kontextmenü oder ein Button angezeigt („Als Zitat einfügen“).
- **Zitat-Integration:**  
  - Beim Klicken:
    - Formatiere den ausgewählten Text als Markdown-Zitat (jedem Zeilenanfang ein `> ` voranstellen).
    - Integriere diesen formatierten Text in die aktuelle Markdown-Notiz im Editor (z. B. an der aktuellen Cursorposition).
  - Nutze hierfür die API des gewählten Editors oder Wails-Methoden zur Interaktion zwischen Frontend-Komponenten.

---

## 7. Export der Markdown-Notiz

- **Export-Mechanismus:**  
  - Biete im Frontend einen „Export“-Button an.
  - Verwende Wails’ Runtime-APIs, z. B. `runtime.SaveFileDialog`, um einen Speicherort auszuwählen.
- **Dateispeicherung:**  
  - Übergebe den Markdown-Text an eine Go-Funktion, die mithilfe von Go’s Datei-I/O-Paketen (`os`, `io/ioutil`) die Datei speichert.
  - Alternativ kann der Export auch direkt im Frontend als Download (über Blob/URL) realisiert werden.

---

## 8. UI-Feedback und Fehlerbehandlung

- **Benutzerfeedback:**  
  - Implementiere visuelle Rückmeldungen für:
    - Erfolgreiche Synchronisation der Tabs
    - Abschluss des Downloads und der Verarbeitung von Webseiten
    - Erfolgreiche Zitatintegration und Export-Vorgänge
  - Verwende Frontend-Benachrichtigungsbibliotheken wie [react-toastify](https://github.com/fkhadra/react-toastify) (bei Verwendung von React) oder vergleichbare Lösungen.
- **Logging und Debugging:**  
  - Implementiere Log-Ausgaben im Backend, um Fehler besser nachvollziehen zu können.
  - Teste alle Funktionalitäten ausgiebig im Entwicklungsmodus mit Wails’ Hot-Reloading.

---

## 9. Testen, Packaging und Deployment

- **Testing:**  
  - Schreibe Unit-Tests für Backend-Funktionen (HTTP-Client, Readability-Extraktion) mit Go’s `testing`-Paket.
  - Führe manuelle Tests für die UI und Integration durch.
- **Packaging:**  
  - Nutze Wails-Build-Tools, um plattformübergreifende ausführbare Dateien zu erstellen.
  - Erstelle Dokumentationen für die Installation und Nutzung der Anwendung.
- **Deployment:**  
  - Erstelle Installationspakete für die Zielplattformen (Windows, macOS, Linux).

---

# Roadmap als Checkliste

- [ ] **Projekt-Setup:**
  - Repository erstellen und Wails-Projekt initialisieren
  - Projektstruktur (Backend/Frontend) festlegen

- [ ] **Browser-Tabs Synchronisation:**
  - Browser-Erweiterung zur Tab-Erfassung entwickeln
  - Kommunikationsschnittstelle (WebSocket oder HTTP) in Go implementieren

- [ ] **Download und Verarbeitung von Webseiten:**
  - HTTP-Download der Seiteninhalte (net/http)
  - Extraktion des Hauptinhalts mittels go-readability
  - Optionale weitere HTML-Verarbeitung mit goquery

- [ ] **Anzeige im vereinfachten Lesemodus:**
  - Frontend-Komponente zur Anzeige des bereinigten HTML-Inhalts entwickeln
  - Ansprechendes CSS-Design implementieren

- [ ] **Integration des Markdown-Editors:**
  - Auswahl und Integration eines Markdown-Editors (SimpleMDE, Toast UI Editor oder CodeMirror)
  - Editor-Konfiguration (Syntax-Hervorhebung, Live-Preview optional)

- [ ] **Text-Hervorhebung und Zitatfunktion:**
  - Event-Listener zur Erfassung von Textselektionen in der Lesemodus-Komponente
  - Zitatformatierung (Markdown-Blockquotes) und Einfügen in den Editor

- [ ] **Export der Markdown-Notiz:**
  - Export-Button im Frontend implementieren
  - Dateiauswahl-Dialog mit Wails’ Runtime-API (SaveFileDialog)
  - Datei-Speicherung im Backend (os, io/ioutil)

- [ ] **UI-Feedback und Fehlerbehandlung:**
  - Benutzerbenachrichtigungen (Erfolg, Fehler) implementieren
  - Backend-Logging und Debugging einrichten

- [ ] **Testen, Packaging und Deployment:**
  - Unit-Tests für Backend-Funktionen schreiben
  - Manuelle UI-Tests und Integrationstests durchführen
  - Anwendung mit Wails für alle Zielplattformen builden und paketieren
