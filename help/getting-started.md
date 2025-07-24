---
title: Erste Schritte mit adaptiven Headless-Formularen
description: Erste Schritte mit adaptiven Headless-Formularen
keywords: Headless, adaptives Formular, Tutorial
hide: true
source-git-commit: 28792fe1690e68cd301a0de2ce8bff53fae1605f
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 50%

---


# Erste Schritte mit Headless Adaptive Forms

Dieses Tutorial bietet Ihnen ein End-to-End-Framework zum Erstellen eines adaptiven Headless-Formulars. Das Tutorial ist in einen Anwendungsfall und mehrere Handbücher unterteilt. Jedes Handbuch hilft Ihnen dabei, neue Funktionen zu erlernen und zum adaptiven Headless-Formular hinzuzufügen, das in diesem Tutorial erstellt wird. Sie verfügen nach jedem Handbuch über ein funktionierendes adaptives Headless-Formular. Am Ende dieses Tutorials sollten Sie zu Folgendem in der Lage sein:

* Erstellen eines adaptiven Headless-Formulars
* Hinzufügen von Geschäftsregeln zum Formular
* Verwenden der Google Material-Benutzeroberfläche zum Formatieren von Formularen
* Vorbefüllen des Formulars
* Einbetten des Formulars in eine Webseite

Sie werden auch ein Verständnis der Architektur, der verfügbaren Artefakte und der JSON-Struktur von Headless-adaptiven Formularen aufbauen.

**Das Ganze beginnt mit dem Kennenlernen des Anwendungsfalls**:

Raya Tan, Mitglied des Außenministeriums eines Landes, das für seine natürliche Schönheit und florierende Tourismuswirtschaft bekannt ist, überwacht die Verteilung von Visaformularen an Touristen. Diese Formulare stehen auf der Website des Ministeriums, in nativen Mobile Apps und im PDF-Format zur Verfügung, mit mehreren Sprachoptionen für die Touristinnen bzw. Touristen zur Auswahl. Die Verwaltung und Skalierung dieser Formulare über verschiedene Plattformen und Technologien hinweg kann jedoch eine Herausforderung darstellen.

Um die Effizienz und Flexibilität ihres Visumantragsverfahrens zu verbessern, hat das Auswärtige Amt beschlossen, einen Ansatz für adaptive Headless-Formulare zu verfolgen. Diese entkoppelte Architektur trennt das Frontend vom Backend, was eine größere Anpassung und Skalierbarkeit ermöglicht. Die Abteilung plant die Verwendung der React-Komponenten der Google Material-Benutzeroberfläche, um das Benutzererlebnis der Formulare zu verbessern. Es werden auch Backend-Funktionen wie die folgenden verwendet:

* Digitale Signaturen
* Datenintegration
* Geschäftsprozessmanagement
* Datensatzdokument
* Nutzungsanalyse

Das beliebteste Formular unter den Touristinnen und Touristen ist das Formular „Kontakt“, das verwendet wird, um verschiedene Fragen und Anfragen zu stellen. Daher hat sich das Auswärtige Amt dafür entschieden, mit der Implementierung des Headless-Ansatzes für adaptive Formulare mit diesem Formular zu beginnen. Dieses Tutorial führt Sie durch den Prozess der Erstellung des Kontakt-Formulars mithilfe dieser neuen Architektur. Das Endergebnis sieht wie folgt aus:

![Adaptives Headless-Formular „Kontakt“](assets/contact-us-headless-adaptive-forms.png)