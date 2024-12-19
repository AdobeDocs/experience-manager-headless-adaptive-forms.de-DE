---
title: Adaptive Headless-Formulare von AEM – Übersicht
description: Übersicht über adaptive Headless-Formulare von AEM.
hide: true
exl-id: cd7c7972-376c-489f-a684-f479d92c37e7
source-git-commit: 0127f8ddede38083f0932b0e8d7efdd0dd77c3a6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Versionshinweise

Willkommen bei der Early-Adopter-Version von adaptiven Headless-Formularen von Experience Manager. Lesen Sie weiter, um Ressourcen und Anweisungen für den Einstieg zu erhalten und das Beste aus der Version zu machen.

Sie können adaptive Headless-Formulare von Adobe Experience Manager verwenden, um Formularanwendungen mithilfe von Frontend-UI-Frameworks wie React, Angular und mehr zu erstellen, und das Adaptive Forms Web SDK für Funktionen wie Statusverwaltung, Validierung und Integrationen mit verschiedenen anderen Touchpoints verwenden.

Die Early-Adopter-Version bietet Ihnen Zugriff auf die Verwendung von adaptiven Headless-Formularen in einer [lokalen Entwicklungsumgebung](setup-development-environment.md). Sie können die lokale Entwicklungsumgebung verwenden, um adaptive Headless-Formulare zu erstellen und zu testen.

Adaptive Headless-Formulare werden laufend verbessert. Besuchen Sie diese Seite regelmäßig, um über die neuesten Entwicklungen auf dem Laufenden zu bleiben. Auf dieser Seite finden Sie Informationen zu frühzeitiger Verfügbarkeit, neuesten Versionen, neuen Funktionen, Verbesserungen, Fehlerbehebungen, veralteten Funktionen, speziellen Anweisungen und zukünftigen Änderungsplänen.

<!-- 

## July 2022 (v0.22.1)

### New features

* Introduced the `validateFormData` API. It validates all the components against the rules and constraints an returns the list of errors. The validation takes place on the server.
* Introduced the `FormLoad` event.
* Introduced the `importData` and `exportData`.
* You can now dynamically add or remove items, that expect unqiue values, from a repeatable panel. You can use the `minItems` and `maxitems` constraint to set limit of item.
* You can now use constraint to set maximum file upload size, accepted file types, minimum files, and maximum files to upload.

### Improvements and bug fixes

* The service was executing some event handlers twice. The issue is fixed.
* Fixing Data Generation with different values of dataRef, name and type.

<!-- ### React Renderer component -->

## Artefakte sind in der Early-Adopter-Version verfügbar

Im Rahmen unseres Bestrebens, Ihnen adaptive Headless-Formulare von Adobe Experience Manager zur Verfügung zu stellen, sind die folgenden Artefakte in der Early-Adopter-Version verfügbar:

### AEM Forms as a Cloud Service SDK

AEM Forms as a Cloud Service SDK hilft Ihnen beim Erstellen, Speichern und Abrufen von adaptiven Headless-Formularen. Es hilft auch bei der Bereitstellung von Vorbefüllung, Server-seitiger Regelvalidierung und Übermittlungsdiensten für adaptive Headless-Formulare.

### Forms Web SDK

Forms Web SDK stellt die APIs zur Validierung von Einschränkungen bereit, die auf verschiedene Felder eines Formulars angewendet werden, sowie Hooks, um die JSON-Struktur des Formulars mit dem UI-Framework zu verbinden. Es bietet außerdem React Renderer für adaptive Headless-Formulare, um die Integration eines adaptiven Headless-Formulars in Ihre Anwendung zu unterstützen. Die folgenden Komponenten des Web SDK sind verfügbar:

* **[@aemforms/af-react-components](https://www.npmjs.com/package/@aemforms/af-react-components)**
* **[@aemforms/af-react-renderer](https://www.npmjs.com/package/@aemforms/af-react-renderer)**
* **[@aemforms/af-core](https://www.npmjs.com/package/@aemforms/af-core)**

<!-- npm i --save @aemforms/af-react-components @aemforms/af-react-renderer @aemforms/af-core -->

#### Storybook

[Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/) bietet einen Überblick über verschiedene Komponenten von adaptiven Headless-Formularen. Außerdem wird eine Liste aller unterstützten Komponenten einschließlich ihrer Eigenschaften und Einschränkungen bereitgestellt.

### Kernkomponenten von Formularen

<!-- Forms components are the structural elements that constitute the content of the form being authored. These components provide various form fields and ability to customize those fields. -->

Kernkomponenten sind eine Reihe standardisierter Web Content Management(WCM)-Komponenten, um die Entwicklungszeit zu verkürzen und die Wartungskosten Ihrer Formulare zu senken. Die Komponente „Formular-Container“ ist eine Kernkomponente. Sie hilft Ihnen, eine JSON-Struktur eines adaptiven Headless-Formulars in den Editor für adaptive Formulare des Forms as a Cloud Service SDK einzubetten und zu rendern.

### Spezifikationen für „Adaptive Formulare V2“

Die Spezifikation für adaptive Headless-Formulare bietet detaillierte Informationen zu allen Komponenten, Einschränkungen und Methoden, die zum Definieren adaptiver Headless-Formulare verfügbar sind. Die Spezifikation ist im [PDF](/help/assets/Headless-Adaptive-Form-Specification.pdf)-Format verfügbar.

### HTTP- und JS-API

[HTTP-APIs](https://opensource.adobe.com/aem-forms-af-runtime/api/) ermöglichen Ihnen das Auflisten, Abrufen, Validieren, Senden und Verfolgen des Übermittlungsstatus von Headless-Formularen. [JS-APIs](https://opensource.adobe.com/aem-forms-af-runtime/jsdocs/) helfen Ihnen, adaptive Headless-Formulare mit jedem JavaScript-basierten UI-Framework zu verwenden.

### Visual Studio Code-Erweiterung

Die [Visual Studio Code-Erweiterung](visual-studio-code-extension-for-headless-adaptive-forms.md) hilft beim Erstellen einer gültigen JSON-Struktur. Sie bietet IntelliSense-Unterstützung und -Validierung für die JSON-Struktur von Formularen sowie allgemeine Funktionen wie das Hinzufügen, Löschen oder Umbenennen von Komponenten einer JSON-Struktur.

<!-- ## What's next

The following features would be available in upcoming releases:

* HTTP APIs to invoke a business logic.
* Server-side capabilities (Prefill, server-side validation, generating Document of Record (DoR), Submitting to a Form Data Model or using Form Data Models for creating rules, and more).
* Continuous improvements to specifications and Headless adaptive form runtime.
* Use  Adaptive Forms editor for easier management and authoring Headless adaptive forms.
-->