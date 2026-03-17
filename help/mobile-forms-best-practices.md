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
source-git-commit: 86129488bec7faed87600a237ac034ca1b601187
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
