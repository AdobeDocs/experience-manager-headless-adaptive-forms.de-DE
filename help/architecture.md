---
title: Architektur von adaptiven Headless-Formularen
description: Erfahren Sie mehr über die Architektur von adaptiven Headless-Formularen in AEM und wie Sie damit schnell Formulare für verschiedene Plattformen erstellen können. Dieser Artikel bietet Einblicke in die Funktionsweise von adaptiven Headless-Formularen und deren Integration in verschiedene Anwendungen, um den Formularerstellungsprozess zu vereinfachen.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
keywords: Headless, adaptives Formular, Architektur
hide: false
exl-id: ee7096d8-89e2-41e0-85e7-b26457df96fb
source-git-commit: c46ac28e490a09d6f563c4b5673d30a53c277a69
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 97%

---


# Wie funktionieren adaptive Headless-Formulare?

Ein adaptives Headless-Formular ist im Wesentlichen eine JSON-Struktur (Schema), die aus Formularfeldern (Textfeld, Auswahl und viele weitere) und entsprechenden Regeln (Bedingungslogik) besteht, um dem Formular interaktives Verhalten hinzuzufügen. Sie können REST-APIs in Ihrer Anwendung oder Website verwenden, um die gehostete JSON-Struktur anzufordern und die JSON-Struktur nativ als Formular in Ihrer App oder Website zu rendern. Ein einzelnes adaptives Headless-Formular kann mehrere Web-Seiten und Anwendungen bedienen, ohne dass App- oder Website-spezifische Änderungen daran vorgenommen werden müssen.

![Funktionsweise von adaptiven Headless-Formularen](/help/assets/how-headless-adaprive-forms-work.png)

## Architektur {#architecture}

Eine typische Architektur für adaptive Headless-Formulare besteht aus einem Adobe Experience Manager Forms-Server, auf diesem Adobe Experience Manager Forms-Server gehosteten adaptiven Headless-Formularen sowie Ihren Frontend-Apps (Website, Mobile App, JavaScript-Apps, Chat-Anwendungen und mehr) für kanalspezifische Formularwiedergaben.

Die typische Architektur einer Bereitstellung von adaptiven Headless-Formularen sieht wie folgt aus:

![Architektur](/help/assets/headless-af-architecture.png)

<!-- 

You can use the React renderer component shipped with Headless adaptive forms to render an Adaptive Form or build your own custom component to natively render a Headless Form in a website or an application or use any UI framework or programming language to build your own components to render your forms.

A typical Headless adaptive forms architecture constitutes an Adobe Experience Manager Server, JSON structure of forms, various frontend apps for channel-specific form renditions.

![Architecture](/help/assets/headless-af-architecture.png) -->

### Komponenten einer Implementierung von adaptiven Headless-Formularen

**Adobe Experience Manager-Server**: Neben der Bereitstellung als Host für adaptive Headless-Formulare bietet Adobe Experience Manager die folgenden Backend-Funktionen:

* RESTful-APIs zum Auflisten, Abrufen, Vorausfüllen, Validieren, Senden und Verfolgen des Übermittlungsstatus von Headless-Formularen.
* Visueller Editor, um adaptive Headless-Formulare einfach zu entwickeln.
* Formulardatenmodell zum Empfangen oder Senden von Daten an verschiedene Datenquellen.
* Workflow-Engine zur Automatisierung komplexer Aufgaben.

**Adaptive Headless-Formulare**: Ein adaptives Headless-Formular wird als JSON-Datei dargestellt. Die JSON-Struktur definiert Komponenten, Einschränkungen und die Struktur eines Formulars.

**Frontend-Apps**: Frontend-Apps wie SPA (Einzelseitenanwendungen), Mobile Apps und JavaScript-Apps verwenden adaptive Headless-Formulare (die JSON-Formulardarstellung) und rendern das Formular auf einem Client. Sie können die React-Renderer-Komponente, die mit adaptiven Headless-Formularen geliefert wird, verwenden, um ein adaptives Formular zu rendern oder Ihre eigene benutzerdefinierte Komponente zu erstellen, um adaptive Headless-Formulare nativ zu rendern.

<!-- ### Understanding Headless adaptive forms definition -->



### Entwickler-Tools

In einem typischen Entwicklungszyklus beginnen Sie mit dem Erstellen und Hosten von adaptiven Headless-Formularen auf dem Adobe Experience Manager Forms-Server. Im zweiten Schritt ordnen Sie Ihre Benutzeroberflächenkomponenten zu oder verwenden eine öffentliche Bibliothek für Benutzeroberflächenkomponenten, wie die Google Material-Benutzeroberfläche oder die Chakra-Benutzeroberfläche, um Ihre Formulare zu gestalten. Im letzten Schritt rufen Sie adaptive Headless-Formulare in Ihrer Anwendung ab und zeigen sie an (Website, Mobile App, JavaScript-Apps, Chat-Anwendungen und viele andere Oberflächen).

Mit den folgenden Tools können Sie adaptive Headless-Formulare erstellen und in Ihre Anwendungen integrieren:

**Forms Web SDK (Client-seitige Laufzeit)**: Das Forms Web SDK ist eine Client-seitige JavaScript-Bibliothek. Damit können Sie Client-seitige Validierungen auf Formularfelder anwenden, den Status des Formulars beibehalten und das Formular mit einer UI-Ebene oder einer gerenderten Komponente für adaptive Formulare verbinden. Es ermöglicht den Kundinnen und Kunden die Validierung von Einschränkungen, die auf verschiedene Felder eines Formulars angewendet werden, und bietet Hooks zur Verbindung der JSON-Struktur des Formulars mit dem UI-Framework. Das Forms Web SDK umfasst die folgenden Komponenten:

* **Verfahrensregelprozessor**: Der Verfahrensregelprozessor akzeptiert die JSON-Struktur der Formulare als Eingabe, verwaltet den Status der Formularfelder und führt Regeln und Ereignis-Handler aus, die in der JSON vorhanden sind.
* **React-Binder**: Stellt Hooks über den Controller bereit, um den Status zu Formularkomponenten hinzuzufügen. Er ist auch beim Vorausfüllen eines Formulars hilfreich.
* **Komponentenbibliothek**: Sie stellt React-Spectrum-Komponenten bereit und verwendet Hooks im React-Binder-Modul, um diesen Komponenten einen Status hinzuzufügen.

Das Forms Web SDK stellt die APIs zur Validierung von Einschränkungen bereit, die auf verschiedene Formularfelder angewendet werden. Außerdem bietet es auch Hooks, um adaptive Headless-Formulare mit dem UI-Framework zu verbinden. Es bietet außerdem React Renderer für adaptive Headless-Formulare, um die Integration eines adaptiven Headless-Formulars in Ihre Anwendung zu unterstützen. Die folgenden Komponenten des Web SDK sind verfügbar:

* **[@aemforms/af-react-components](https://www.npmjs.com/package/@aemforms/af-react-components)**
* **[@aemforms/af-react-renderer](https://www.npmjs.com/package/@aemforms/af-react-renderer)**
* **[@aemforms/af-core](https://www.npmjs.com/package/@aemforms/af-core)**

Alle diese Komponenten sind im AEM-Archetyp enthalten. Wenn Sie mit dem AEM-Archetyp 37 oder später ein Projekt für adaptive Headless-Formulare erstellen, ist die neueste Version der oben aufgeführten Bibliotheken im Projekt enthalten.

* **Code-Playground**: [Code-Playground](https://experienceleague.adobe.com/landing/aem-headless-forms/developer/code.html?lang=en) ist eine interaktive Umgebung, in der Entwicklerinnen und Entwickler die Funktionen von Headless Adaptive Forms experimentieren, kennenlernen und testen können.

**Starter Application**: Adobe hat auch eine Anwendung für die ersten Schritte veröffentlicht, die Ihnen dabei hilft, schnell mit adaptiven Headless-Formularen zu beginnen.

<!-- **View Library (UI Layer)**: A custom form application built in a front-end language. You can use react, Angular, Flutter, NPM, Vue.js, Ionic, BootStrap, or any other language to built front end. You can also use the Headless adaptive forms Super Component, provided out-of-the-box, inside a react application to render a Headless adaptive form. Headless adaptive forms super component makes use of OOTB react spectrum -based form components to render the Headless adaptive form. 

Core-Components: It enables use to render an Adaptive Form using JSON structure. It uses rule grammar to help create dynamic field interactions. The rule grammar is based on [JSON formula](http://github.com/adobe/json-formula/). You can develop your own renderer or embed the React based Adaptive Forms renderer, provided OOTB, in your front-end app to render the form. -->

**Storybook**: [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/) bietet einen Überblick über verschiedene Komponenten von adaptiven Headless-Formularen. Außerdem wird eine Liste aller unterstützten Komponenten einschließlich ihrer Eigenschaften und Einschränkungen bereitgestellt.

**Visual Studio Code-Erweiterung**: [Visual Studio Code-Erweiterung](visual-studio-code-extension-for-headless-adaptive-forms.md) zur Unterstützung beim Erstellen einer gültigen JSON-Struktur. Sie bietet IntelliSense-Unterstützung und -Validierung für die JSON-Struktur von Formularen sowie allgemeine Funktionen wie das Hinzufügen, Löschen oder Umbenennen von Komponenten in einer JSON-Struktur.

**HTTP- und JavaScript-APIs**: [HTTP-APIs](https://opensource.adobe.com/aem-forms-af-runtime/api/) ermöglichen Ihnen das Auflisten, Abrufen, Validieren, Senden und Verfolgen des Übermittlungsstatus von Headless-Formularen. [JS-APIs](https://opensource.adobe.com/aem-forms-af-runtime/jsdocs/) helfen Ihnen, adaptive Headless-Formulare mit jedem JavaScript-basierten UI-Framework zu verwenden.

**JSON-Formel**: Hierbei handelt es sich um eine Implementierung der Grammatik von Formularausdrücken, die Sie beim Abfragen der JSON-Struktur und beim Erstellen von Regeln für adaptive Headless-Formulare unterstützt. Die Grammatik ist eine Mischung aus tabellenähnlichen Funktionen und Operatoren und [JMESPath](https://jmespath.org/), einer JSON-Abfragesprache. Sie können den [Spielplatz](https://opensource.adobe.com/json-formula/dist/index.html) nutzen, um die Syntax und Funktionen der JSON-Formeln auszuprobieren.

**Adaptive Formulare Version 2.0 – Spezifikation**: Die Spezifikation für adaptive Formulare Version 2.0 bietet detaillierte Informationen zu allen Komponenten, Einschränkungen und Methoden, die zum Definieren adaptiver Headless-Formulare verfügbar sind. Die Spezifikation ist im [PDF](/help/assets/headless-adaptive-forms-specification.pdf)-Format verfügbar.

