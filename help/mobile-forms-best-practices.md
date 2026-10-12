---
title: Best Practices für Mobile Forms
description: Für Anwendungsfälle für mobile und Offline-Formulare erstellen Sie Ihre eigene native App und rufen Formulardefinitionen über die Headless Adaptive Forms-API ab. Empfohlener Ansatz für native Mobile Apps.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
keywords: Mobile Forms, native App, Offline-Formulare, Headless-API
index: true
exl-id: 6f25039f-61fc-4366-9e17-6b2809162c58
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: b34afbc4f692b81838ad6947895c9b347dff6d62
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 5%
---
# Best Practices für Mobile Forms {#mobile-forms-best-practices}

Für Anwendungsfälle von mobilen und Offline-Formularen wird empfohlen, eine eigene native App zu erstellen und Formulardefinitionen über die Headless Adaptive Forms-API abzurufen. Dadurch erhalten Sie die volle Kontrolle über das mobile Erlebnis und die kontinuierliche Unterstützung bei der Weiterentwicklung mobiler Plattformen.

## Empfohlener Ansatz {#recommended-approach}

Erstellen Sie eine native Mobile App (iOS oder Android), die:

1. **Ruft die Headless-Formulardefinition ab** - Verwenden Sie die [Headless Adaptive Forms APIs](https://opensource.adobe.com/aem-forms-af-runtime/api/), um das Formular JSON bei Bedarf abzurufen (z. B. wenn der Benutzer ein Formular öffnet oder zu ihm in Ihrer App navigiert). Sie können verfügbare Formulare auflisten und dann die Formulardefinition nach ID abrufen.

2. **Rendern des Formulars in Ihrer App** - Verwenden Sie Ihr bevorzugtes UI-Framework (z. B. React Native oder native Ansichten), um das Formular aus JSON zu rendern. Sie können die Forms Web SDK und bestehende React-Komponenten für adaptive Headless-Formulare verwenden, wo sie zu Ihrem Stack passen, oder Sie können Ihren eigenen Renderer erstellen, der dieselbe JSON-Struktur nutzt.

3. **Unterstützt optional offline** - Implementieren Sie lokalen Speicher und die Synchronisierung in Ihrer App. Speichern Sie beispielsweise Formulardefinitionen im Online-Modus zwischen, speichern Sie Entwürfe lokal und senden oder synchronisieren Sie Daten, wenn das Gerät wieder online ist.

Dieser Ansatz sorgt dafür, dass Ihre App auch dann wartbar bleibt, wenn sich Android und iOS ändern, und verwendet die unterstützte Headless Adaptive Forms-Plattform für die Formularerstellung, -validierung und -übermittlung.

## Erste Schritte {#getting-started}

* [Übersicht über adaptive AEM Headless-](overview.md) - Funktionen und Konzepte.
* [APIs für adaptive Headless-Formulare](https://opensource.adobe.com/aem-forms-af-runtime/api/) - Formulare programmgesteuert auflisten, abrufen, validieren und senden.
* [Architektur](architecture.md) - So funktionieren Headless-adaptive Formulare und wie sie von Frontend-Apps genutzt werden.

Eine schrittweise Integration finden Sie unter [Erstellen und Veröffentlichen eines Headless-Formulars](create-and-publish-a-headless-form.md) und im [Entwicklerportal](https://experienceleague.adobe.com/landing/aem-headless-forms/developer.html?lang=de).
