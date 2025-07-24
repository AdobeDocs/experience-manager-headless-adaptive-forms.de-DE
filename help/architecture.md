---
title: Architektur von adaptiven Headless-Formularen
description: Erfahren Sie mehr über die Architektur von AEM Forms Headless Adaptive Forms und wie Sie damit schnell Formulare für verschiedene Plattformen erstellen können. Dieser Artikel bietet Einblicke in die Funktionsweise von Headless Adaptive Forms und wie sie in verschiedene Programme integriert werden können, um den Prozess der Formularerstellung zu vereinfachen.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
keywords: Headless, adaptives Formular, Architektur
hide: false
exl-id: ee7096d8-89e2-41e0-85e7-b26457df96fb
source-git-commit: 28792fe1690e68cd301a0de2ce8bff53fae1605f
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 54%

---


# Wie funktionieren adaptive Headless-Formulare?

Ein adaptives Headless-Formular ist im Wesentlichen eine JSON-Struktur (Schema), die aus Formularfeldern (Textfeld, Auswahlmöglichkeiten und viele weitere Felder) und entsprechenden Regeln (bedingte Logik) besteht, um dem Formular interaktives Verhalten hinzuzufügen. Sie können REST-APIs in Ihrer Anwendung oder Website verwenden, um die gehostete JSON-Struktur anzufordern und die JSON-Struktur nativ als Formular in Ihrer App oder Website zu rendern. Ein einzelnes adaptives Headless-Formular kann mehrere Web-Seiten und Anwendungen bedienen, ohne dass App- oder Website-spezifische Änderungen daran vorgenommen werden müssen.

![Funktionsweise von adaptiven Headless-Formularen](/help/assets/how-headless-adaprive-forms-work.png)

## Architektur {#architecture}

Eine typische Architektur für adaptive Headless-Formulare basiert auf einem Adobe Experience Manager Forms-Server, der Headless-adaptive Formulare hostet. Frontend-Apps - Web, Mobile, JavaScript, Chatbots und mehr - rendern die Formulare für jeden Kanal.

Die typische Architektur einer Bereitstellung adaptiver Headless-Formulare sieht wie folgt aus:

![Architektur](/help/assets/headless-af-architecture.png)

<!-- 

You can use the React renderer component shipped with Headless adaptive forms to render an Adaptive Form or build your own custom component to natively render a Headless Form in a website or an application or use any UI framework or programming language to build your own components to render your forms.

A typical Headless adaptive forms architecture constitutes an Adobe Experience Manager Server, JSON structure of forms, various frontend apps for channel-specific form renditions.

![Architecture](/help/assets/headless-af-architecture.png) -->

### Komponenten einer Implementierung von adaptiven Headless-Formularen

**Adobe Experience Manager-Server**: Neben der Bereitstellung als Host für adaptive Headless-Formulare bietet Adobe Experience Manager die folgenden Backend-Funktionen:

* RESTful-APIs zum Auflisten, Abrufen, Vorausfüllen, Validieren, Übermitteln und Nachverfolgen des Übermittlungsstatus von Headless-Formularen.
* Visual Editor zum einfachen Entwickeln eines adaptiven Headless-Formulars.
* Formulardatenmodell zum Empfangen oder Senden von Daten an verschiedene Datenquellen.
* Eine Workflow-Engine zur Automatisierung komplexer Aufgaben.

**Adaptive Headless-Formulare**: Ein adaptives Headless-Formular wird als JSON-Datei dargestellt. Die JSON-Struktur definiert Komponenten, Einschränkungen und die Struktur eines Formulars.

**Frontend-Apps**: Frontend-Apps wie SPA (Einzelseitenanwendungen), Mobile Apps und JavaScript-Apps verwenden adaptive Headless-Formulare (die JSON-Formulardarstellung) und rendern das Formular auf einem Client. Sie können die React-Renderer-Komponente verwenden, die mit adaptiven Headless-Formularen bereitgestellt wird, um ein adaptives Formular zu rendern, oder Ihre eigene benutzerdefinierte Komponente erstellen, um Headless-adaptive Formulare nativ zu rendern.

<!-- ### Understanding Headless adaptive forms definition -->



### Entwickler-Tools

In einem typischen Entwicklungszyklus beginnen Sie mit dem Erstellen und Hosten von adaptiven Headless-Formularen auf dem Adobe Experience Manager Forms-Server. Im zweiten Schritt ordnen Sie Ihre Benutzeroberflächenkomponenten zu oder verwenden eine öffentliche Bibliothek für Benutzeroberflächenkomponenten, wie die Google Material-Benutzeroberfläche oder die Chakra-Benutzeroberfläche, um Ihre Formulare zu gestalten. Im letzten Schritt rufen Sie adaptive Headless-Formulare in Ihrer Anwendung ab und zeigen sie an (Website, Mobile App, JavaScript-Apps, Chat-Anwendungen und viele andere Oberflächen).

Mit den folgenden Tools können Sie adaptive Headless-Formulare erstellen und in Ihre Anwendungen integrieren:

**Forms Web SDK (Client-seitige Laufzeit)**: Das Forms Web SDK ist eine Client-seitige JavaScript-Bibliothek. Sie ermöglicht es Ihnen, Client-seitige Validierungen auf Formularfelder anzuwenden, den Status des Formulars beizubehalten und stellt Erweiterungspunkte zum Verbinden des Formulars mit der Ebene der Benutzeroberfläche oder der gerenderten Komponente für adaptive Formulare bereit. Damit können Kunden Einschränkungen, die auf verschiedene Felder eines Formulars angewendet werden, validieren und Erweiterungspunkte (Hooks) nutzen, um die JSON-Struktur des Formulars mit dem UI-Framework zu verbinden. Das Forms Web SDK umfasst die folgenden Komponenten:

* **Verfahrensregelprozessor**: Der Verfahrensregelprozessor akzeptiert die JSON-Struktur der Formulare als Eingabe, verwaltet den Status der Formularfelder und führt Regeln und Ereignis-Handler aus, die in der JSON vorhanden sind.
* **React-Binder**: Stellt Hooks über den Controller bereit, um den Status zu Formularkomponenten hinzuzufügen. Er ist auch beim Vorausfüllen eines Formulars hilfreich.
* **Komponentenbibliothek**: Sie stellt React Spectrum-Komponenten bereit und verwendet Erweiterungspunkte (Hooks) im React Binder-Modul, um den Status dieser Komponenten hinzuzufügen.

Das Forms Web SDK stellt die APIs zur Validierung von Einschränkungen bereit, die auf verschiedene Formularfelder angewendet werden. Außerdem bietet es auch Hooks, um adaptive Headless-Formulare mit dem UI-Framework zu verbinden. Außerdem bietet es einen React-Renderer für adaptive Headless-Formulare, um ein adaptives Headless-Formular in Ihre Anwendung zu integrieren. Die folgenden Komponenten der Web-SDK sind verfügbar:

* **[@aemforms/af-react-components](https://www.npmjs.com/package/@aemforms/af-react-components)**
* **[@aemforms/af-react-renderer](https://www.npmjs.com/package/@aemforms/af-react-renderer)**
* **[@aemforms/af-core](https://www.npmjs.com/package/@aemforms/af-core)**

Alle diese Komponenten sind im AEM-Archetyp enthalten. Wenn Sie ein AEM-Archetyp 37- oder neueres Projekt für Headless-adaptive Formulare erstellen, wird die neueste Version der oben aufgeführten Bibliotheken in das Projekt aufgenommen.

* **Code-Playground**: [Code-Playground](https://experienceleague.adobe.com/landing/aem-headless-forms/developer/code.html?lang=de) ist eine interaktive Umgebung, in der Entwickler mit den Funktionen von Headless Adaptive Forms experimentieren, mehr darüber erfahren und sie testen können.

**Starter Application**: Adobe hat auch eine Anwendung für die ersten Schritte veröffentlicht, die Ihnen dabei hilft, schnell mit adaptiven Headless-Formularen zu beginnen.

<!-- **View Library (UI Layer)**: A custom form application built in a front-end language. You can use react, Angular, Flutter, NPM, Vue.js, Ionic, BootStrap, or any other language to built front end. You can also use the Headless adaptive forms Super Component, provided out-of-the-box, inside a react application to render a Headless adaptive form. Headless adaptive forms super component makes use of OOTB react spectrum -based form components to render the Headless adaptive form. 

Core-Components: It enables use to render an Adaptive Form using JSON structure. It uses rule grammar to help create dynamic field interactions. The rule grammar is based on [JSON formula](http://github.com/adobe/json-formula/). You can develop your own renderer or embed the React based Adaptive Forms renderer, provided OOTB, in your front-end app to render the form. -->

**Storybook**: [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/) bietet einen Überblick über verschiedene Komponenten von adaptiven Headless-Formularen. Außerdem wird eine Liste aller unterstützten Komponenten einschließlich ihrer Eigenschaften und Einschränkungen bereitgestellt.

**Visual Studio Code-Erweiterung**: [Visual Studio Code-Erweiterung](visual-studio-code-extension-for-headless-adaptive-forms.md) zur Unterstützung beim Erstellen einer gültigen JSON-Struktur. Sie bietet IntelliSense-Unterstützung und -Validierung für die JSON-Struktur von Formularen sowie allgemeine Funktionen wie das Hinzufügen, Löschen oder Umbenennen von Komponenten in einer JSON-Struktur.

**HTTP- und JavaScript**-APIs[ Mit HTTP-APIs](https://opensource.adobe.com/aem-forms-af-runtime/api/) können Sie den Übermittlungsstatus von Headless-Formularen auflisten, abrufen, validieren, senden und verfolgen. <!-- URL is 404!! [JS APIs](https://opensource.adobe.com/aem-forms-af-runtime/jsdocs/) helps you use Headless adaptive forms with any JavaScript based UI framework. -->

**JSON-Formel**: Hierbei handelt es sich um eine Implementierung der Grammatik von Formularausdrücken, mit der Sie die JSON-Struktur abfragen und Regeln für adaptive Headless-Formulare erstellen können. Die Grammatik ist eine Mischung aus tabellenähnlichen Funktionen und Operatoren und [JMESPath](https://jmespath.org/), einer JSON-Abfragesprache. Sie können den [Spielplatz](https://opensource.adobe.com/json-formula/dist/index.html) nutzen, um die Syntax und Funktionen der JSON-Formeln auszuprobieren.

**Spezifikationen von Adaptive Forms Version 2.0**: Die Spezifikation von Adaptive Forms Version 2.0 enthält detaillierte Informationen zu allen Komponenten, Einschränkungen und Methoden, die zum Definieren adaptiver Headless-Formulare verfügbar sind. Die Spezifikation ist im [PDF](/help/assets/headless-adaptive-forms-specification.pdf)-Format verfügbar.

