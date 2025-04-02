# Implementierungsplan

Dieses Dokument beschreibt schrittweise, wie eine Java/JavaFX-Anwendung umgesetzt werden kann, die Browser-Tabs synchronisiert, Webseiten im Lesemodus darstellt und das Erstellen von Markdown-Notizen mit Zitierfunktion erlaubt. Dabei wird auf notwendige Bibliotheken, Lerninhalte und Aufgaben eingegangen.

---

## 1. Projektübersicht

**Ziel**

- Synchronisieren von offenen Browser-Tabs (bzw. Links) mit der Java-Anwendung.
    
- Herunterladen der Inhalte und Darstellen im Lesemodus (reduzierte, lesefreundliche Ansicht).
    
- Markieren von Textstellen auf der dargestellten Seite und Übernahme als Zitat in eine Markdown-Notiz.
    
- Möglichkeit, diese Notizen zu exportieren (z. B. als Markdown-Datei oder PDF).
    

**Technologiestack**

- **Programmiersprache**: Java (z. B. Java 17 oder neuer)
    
- **UI-Framework**: JavaFX (z. B. OpenJFX)
    
- **Weitere Bibliotheken**
    
    - **HTML-Parsing**: [JSoup](https://jsoup.org/) (zum Extrahieren/Vereinfachen von HTML)
        
    - **Markdown-Verarbeitung**: [Flexmark](https://github.com/vsch/flexmark-java) oder [CommonMark](https://github.com/commonmark/commonmark-java)
        
    - **PDF-Export** (optional): [Apache PDFBox](https://pdfbox.apache.org/) oder [iText](https://itextpdf.com/)
        
    - **Datenpersistenz**: z. B. SQLite oder JSON-Dateien (falls benötigt)
        

---

## 2. Voraussetzungen & Lernbedarf

1. **Java & OOP**
    
    - Objektorientierte Programmierung (Klassen, Interfaces, Design-Patterns)
        
    - Paket- und Build-Management (Maven oder Gradle)
        
2. **JavaFX**
    
    - Grundlagen in JavaFX (Aufbau von UI-Komponenten wie Buttons, TextArea, WebView, etc.)
        
    - (Optional) FXML zur Trennung von Layout und Logik
        
3. **HTML-Parsing / Lesemodus**
    
    - Verwendung von JSoup zum Parsen und Vereinfachem von HTML
        
4. **Markdown**
    
    - Grundkenntnisse der Syntax
        
    - Nutzung einer Bibliothek (z. B. Flexmark), um Markdown zu parsen oder zu rendern
        
5. **Synchronisationsmechanismus**
    
    - Browser-Plugin oder Export-Funktion für Tabs
        
    - Lokale Speicherung (Datei oder Datenbank)
        
6. **Exportfunktion**
    
    - PDF-Generierung (PDFBox/iText) oder einfacher Markdown-Export
        

---

## 3. Grobarchitektur

1. **Backend-Logik (Java)**
    
    - Service zum Empfangen und Speichern der Tab-Informationen
        
    - Service/Komponente zum Herunterladen und Parsen der Webseiten
        
    - Service für Markdown-Notizen (Verwaltung, Export, Zitate einfügen)
        
2. **Frontend (JavaFX)**
    
    - Hauptfenster mit
        
        - Seitenübersicht (Liste der synchronisierten Webseiten)
            
        - Darstellungsbereich im Lesemodus (WebView oder Text-Container)
            
        - Editorbereich (Markdown) für Notizen
            
    - Möglichkeit, Textstellen zu markieren und als Zitat in den Editor zu übernehmen
        
3. **Datenhaltung**
    
    - Optional: In-Memory oder lokal (Datei/SQLite)
        

---

## 4. Schritt-für-Schritt-Implementierung

### 4.1 Projektstruktur einrichten

-  **Java-Projekt aufsetzen** (Maven oder Gradle)
    
-  **JavaFX-Abhängigkeit** integrieren (z. B. über Maven Central)
    
-  **Weitere Libraries** (JSoup, Flexmark/CommonMark, PDFBox/iText) hinzufügen
    

### 4.2 Browser-Tabs synchronisieren

> Die konkrete Umsetzung hängt stark davon ab, wie man an die Browser-Tabs gelangt. Mögliche Ansätze sind ein Browser-Plugin (Chrome, Firefox), das die offenen Tabs via HTTP oder Datei-Export an die Java-App übergibt.

-  **Browser-Plugin** oder **API** entwickeln, das die offenen Tabs sammelt.
    
-  **Empfangsservice in Java** oder einfacher **Dateiimport** (JSON, CSV, o. ä.):
    
    - **Plugin-Variante**: Minimalistischer HTTP-Server (z. B. [NanoHTTPD](https://github.com/NanoHttpd/nanohttpd)) in der Java-Anwendung.
        
    - **Datei-Variante**: JSON-Export aus dem Browser, den die JavaFX-App einlesen kann.
        
-  **Speichern der Links** (z. B. in einer `List<TabInfo>`)
    

### 4.3 Datenmodell erstellen

-  **Klasse `TabInfo`**:
    

```java
public class TabInfo {
    private String url;
    private String title;
    // Weitere Felder je nach Bedarf

    // Konstruktor, Getter, Setter
}
```

-  **Klasse `Article`** (optional), wenn man den Inhalt lokal zwischenspeichern möchte:
    

```java
public class Article {
    private String url;
    private String title;
    private String content; // Gesäubertes HTML für den Lesemodus
    
    // Konstruktor, Getter, Setter
}
```

### 4.4 GUI-Struktur (JavaFX)

-  **Main-App-Klasse** (z. B. `MainApp extends Application`) mit `start(Stage primaryStage)`.
    
-  **Layout**:
    
    - Hauptfenster mit einem `BorderPane` oder `SplitPane`:
        
        - **Linke Seite**: Liste aller synchronisierten Tabs (z. B. `ListView<TabInfo>`)
            
        - **Mitte**: `WebView` (oder TextContainer) zur Darstellung des Artikels
            
        - **Rechte Seite**: Markdown-Editor (`TextArea` oder ein spezielles Editor-Widget)
            
-  **Event-Handling**:
    
    - Klick in der Tab-Liste → Lade und zeige Inhalt im Lesemodus
        
    - Schaltflächen, um Textstellen zu markieren und ins Markdown einzufügen
        

### 4.5 Lesemodus implementieren

1. **Webseiten herunterladen**
    
    -  Bei Auswahl eines Tabs: `Document doc = Jsoup.connect(url).get();`
        
    -  HTML parsen
        
2. **HTML vereinfachen** (optional)
    
    -  Unnötige Skripte, Ads entfernen
        
    -  Nur den `<body>` und relevante Elemente beibehalten
        
3. **Anzeigen im `WebView`**
    
    -  `webView.getEngine().loadContent(cleanedHtml, "text/html");`
        

### 4.6 Markieren von Textstellen & Zitieren

-  **Konzept**
    
    - Text wird im `WebView` markiert
        
    - Ein Button (z. B. "Als Zitat übernehmen") liest den markierten Text aus und fügt ihn als Markdown-Zitat ein
        
-  **Realisierung**
    
    ```java
    String selectedText = 
        (String) webView.getEngine().executeScript("window.getSelection().toString();");
    // Dann in den Editor einfügen, z. B.:
    markdownEditor.appendText("> " + selectedText + "\n");
    ```
    

### 4.7 Markdown-Editor

-  **TextArea** für Markdown
    
    - Einfache Lösung: normale `TextArea`
        
    - (Optional) [RichTextFX](https://github.com/FXMisc/RichTextFX) für Syntax-Highlighting
        
-  **Live-Vorschau (optional)**
    
    - Z. B. eine zweite `WebView`, in der mittels Flexmark das Markdown gerendert wird
        

### 4.8 Exportfunktion

-  **Markdown-Datei**
    
    - Einfach: Inhalt als `.md`-Datei speichern
        
    - FileChooser oder "Speichern unter" verwenden
        
-  **PDF-Erzeugung (optional)**
    
    -  Markdown → HTML mit Flexmark
        
    -  HTML → PDF mit iText oder PDFBox
        
    -  Über einen Dialog abspeichern
        

### 4.9 Datenpersistenz (optional/erweitert)

-  **SQLite oder JSON**
    
    - Alle Notizen und Links beim Beenden speichern
        
    - Beim Neustart laden
        

### 4.10 Testen und Debuggen

-  **Komponententests** (HTML-Parsing, Synchronisation)
    
-  **GUI-Tests** (Benutzereingaben, Notizverwaltung)
    
-  **Fehlerszenarien** (kein Netzwerk, ungültige URL, etc.)
    

---

## 5. Detaillierte Checkliste

### **Planungsphase**

-  Anforderungen definieren (Browser, Exportformate, Offline-Nutzung, etc.)
    
-  Browser-Plugin-APIs recherchieren (Chrome, Firefox)
    

### **Einrichten der Entwicklungsumgebung**

-  Java 17+ installieren (OpenJDK o. Ä.)
    
-  JavaFX (OpenJFX) bereitstellen
    
-  IDE-Konfiguration (IntelliJ, Eclipse, NetBeans)
    

### **Basisprojekt erstellen**

-  Maven/Gradle-Konfiguration (pom.xml / build.gradle)
    
-  Hauptklasse `MainApp` (JavaFX `Application`)
    
-  FXML-Datei (optional) erstellen
    

### **Synchronisations-Ansatz klären**

-  Browser-Plugin vs. Dateiimport
    
-  Netzwerk oder Dateisystem
    

### **Grundfunktionen in der JavaFX-Anwendung**

-  Liste/TreeView für Webseiten
    
-  WebView für Inhalt
    
-  Editor für Markdown-Notizen
    

### **Lesemodus**

-  JSoup-Prototyp
    
-  HTML vereinfachen
    
-  Im WebView anzeigen
    

### **Markierung & Zitatfunktion**

-  Selektion im WebView auslesen
    
-  Zitat als Markdown einfügen
    

### **Notizenverwaltung**

-  Speichern und Laden der Notizen
    
-  Export als Markdown
    

### **(Optional) PDF-Export**

-  Markdown → HTML
    
-  HTML → PDF
    

### **Testen & Verfeinern**

-  Funktionstests
    
-  GUI-Tests
    
-  Bugfixing
    

---

## 6. Weiterführende Ideen

- **Offline-Fähigkeit**: Vollständiges Herunterladen der Seite für Offline-Lesen
    
- **Multi-Plattform**: JavaFX läuft auf Windows, macOS, Linux
    
- **Erweiterte Formatierung**: Syntax-Highlighting, Themes für Editor
    
- **Cloud-Synchronisation**: Dropbox, Google Drive
    
- **Browser-Integration**: Automatische Übernahme markierter Textstellen direkt vom Plugin
    

---

## Fazit

Mit diesem Plan erhältst du eine solide Grundlage, um die Java/JavaFX-Anwendung umzusetzen. Die wesentlichen Schritte sind:

1. **Browser-Tabs holen** (Plugin/Export)
    
2. **Webseiten im Lesemodus** (JSoup + JavaFX-WebView)
    
3. **Markdown-Editor** inkl. Zitierfunktion
    
4. (Optional) **Export** als Markdown oder PDF
    

Viel Erfolg bei der Umsetzung!