---
title: Häufig gestellte Fragen zu Headless Adaptive Forms
description: Häufig gestellte Fragen
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
keywords: headless, adaptives Formular, FAQ
hide: false
exl-id: 5bfc307d-96a3-4007-b65f-32176ecdb710
source-git-commit: 28792fe1690e68cd301a0de2ce8bff53fae1605f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 69%

---

# Häufig gestellte Fragen (FAQ) {#headless-adaptive-forms-faq}

## Sollte ich wissen, dass React.js Headless-adaptive Formulare verwendet?

Sie können jedes Framework, jede Bibliothek und jede Sprache verwenden, um adaptive Headless-Formulare zu rendern und die REST-APIs von Adobe zu verwenden, um die Formulare zu validieren und zu senden. Die AF-Core-Bibliothek, die Ihnen standardmäßig bereitgestellt wird, ist Framework-unabhängig. Die React-Render- und React-Komponentenbibliotheken, die Ihnen vorkonfiguriert bereitgestellt werden, dienen der Vereinfachung. Sie können Ihre eigenen Komponenten erstellen; Sie sind nicht auf die bereitgestellten Komponenten beschränkt.


<!-- 
## Did Adobe release a new AEM Archetype for Headless adaptive forms?

You can use Archetype 37 with flag `includeFormsheadless` or later flag to create an AEM project with Headless adaptive forms functionality. 

-->

## Benötige ich eine Forms as a Cloud Service-Sandbox, um adaptive Headless-Formulare zu verwenden?

Mit der Starter-App können Sie mit der Entwicklung und Gestaltung Ihrer adaptiven Headless-Formulare beginnen. Sie benötigen Forms as a Cloud Service, um adaptive Headless-Formulare zusammen mit Backend-Formularfunktionen zu hosten und bereitzustellen.

<!-- ## Do I need an archetype project to develop Headless adaptive forms?

You can use the starter app to start developing and styling your Headless adaptive forms. Later on, you can use the 
archetype project to deploy the finished Headless adaptive forms and corresponding custom code, created using starter app, to Forms as a Cloud Service environment. The Forms as a Cloud Service environment helps you test and productionize the forms. -->

## Wo erhalte ich eine Vorschau eines adaptiven Headless-Formulars? {#storybook-example}

Mit der Starter-App können Sie ein benutzerdefiniertes adaptives Headless-Formular rendern und in der Vorschau anzeigen. Sie können auch ein Beispiel für ein [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-examples--introduction) zur Vorschau eines adaptiven Headless-Formulars bearbeiten.

![](/help/assets/storybook-example.png)

## Ist es möglich, adaptive Headless-Formulate mit benutzerdefinierten Frameworks zu verwenden?

Adaptive Headless-Formulare basieren auf einer [Standardspezifikation](/help/assets/headless-adaptive-forms-specification.pdf). Sie können die Spezifikation erweitern, um sie zum Erstellen benutzerdefinierter Komponenten zu verwenden. Zum Beispiel Komponenten für Chakra UI, Vue.js und mehr.

## Unterstützen adaptive Headless-Formulare kaskadierende Felder?

In kaskadierenden Feldern hängt der Inhalt des zweiten Felds von dem im ersten Feld ausgewählten Inhalt ab. Das [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/adaptive-form-dynamic-behaviour--options&args=formJson.items[0].fieldType:drop-down;formJson.items[0].minimum:!undefined;formJson.items[0].maximum:!undefined;formJson.items[0].label.value:Choose+number+of+options;formJson.items[0].enum[0]:1;formJson.items[0].enum[1]:2;formJson.items[0].enum[2]:3;formJson.items[1].fieldType:drop-down) bietet ein Beispiel für kaskadierende Felder.

## Ermöglichen adaptive Headless-Formulare das Vorausfüllen von Formularen mit personalisierten Daten?

Headless Adaptive Forms ermöglichen das Vorbefüllen von Formularen mit personalisierten Daten. Das [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-examples--prefill-form-with-personalised-data) bietet ein Beispiel dafür, wie ein adaptives Headless-Formular vorab ausgefüllt werden kann.

<!-- >
## Can I use existing Adaptive Forms editor to create a Headless adaptive form?

At this moment, you use the Adaptive Form Editor to specify the JSON structure and set submit action for the forms. Support for drag-and-drop components, applying rules using editor, and more editor-related options would be available later in the beta phase. Keep a watch on release notes.  -->

## Kann ich adaptive Headless-Formulare mit Angular SPA verwenden?

Sie können das Web SDK verwenden, um adaptive Headless-Formulare in Angular SPA zu integrieren. Es ist unabhängig von jeglichem Framework. Sie können die React-SDK als Referenz verwenden.

<!-- ## Should the `-r prerelease` switch be used every time to start the AEM SDK instance or only for the first time?

During the limited release program, use the `-r prerelease` switch every time you start the AEM SDK instance. 

## What is AEM Forms add-on (.far file) and how to install it?

Adobe Experience Manager Forms as a Cloud Service feature archive provides tools to create Headless adaptive forms on the local development environment. To install the feature archive, see [Setup development environment](setup-development-environment.md).

<!-- 
## Where do one get the license.properties file from?

You do not require a license.properties file to run AEM Cloud Service SDK. 

-->

## Gibt es ein Plugin, das die Entwicklung von Headless AF erleichtert?

Ja - Mit einer Visual Studio Code-Erweiterung können Sie adaptive Headless-Formulare manuell in JSON erstellen.

## Kann ein adaptives Headless-Formular eine Verbindung zu jedem CRM herstellen, um Daten zu lesen oder zu schreiben?

Sie können Microsoft Dynamics und Salesforce verwenden, um ein adaptives Headless-Formular zu übermitteln oder vorab auszufüllen. Abgesehen von CRMs unterstützen adaptive Headless-Formulare das Senden oder Vorabausfüllen mithilfe von REST-Endpunkten, E-Mails und benutzerdefinierte Übermittlungsaktionen.
