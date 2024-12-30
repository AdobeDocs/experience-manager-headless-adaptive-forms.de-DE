---
title: Visual Studio Code-Erweiterung für adaptive Headless-Formulare
description: Visual Studio Code-Erweiterung für adaptive Headless-Formulare
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
keywords: Headless, adaptive Formulare, Visual Studio Code-Erweiterung
hide: false
exl-id: 11960e91-6c09-48d4-9d57-37537f808cd4
source-git-commit: 47ac7d03c8c4fa18ac3bdcef04352fdd1cad1b16
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 100%

---

# Microsoft Visual Studio Code-Erweiterung für adaptive Headless-Formulare

Wenn Sie Microsoft® Visual Studio Code als IDE verwenden, können Sie die Microsoft Visual Studio Code-Erweiterung für adaptive Formulare verwenden. Die Erweiterung:

* Fügt IntelliSense-Funktionen für adaptive Formulare zu Visual Studio-Code hinzu
* Hilft bei der Validierung und automatischen Vervollständigung der JSON-Syntax für Komponenten adaptiver Headless-Formulare
* Bietet ein Bedienfeld zum einfachen Navigieren in der Struktur für ein adaptives Headless-Formular
* Hilft bei der Übersetzung eines adaptiven Headless-Formulars

<!-- 

The extension o easily navigate the structure 

Adobe provides an extension for Microsoft&reg; Visual Studio Code to make it easier for you to navigate structure and develop Headless adaptive forms in Visual Studio Code. The extension adds Adaptive Forms related IntelliSense capabilities and helps auto-complete Headless adaptive forms JSON syntax. It also adds a panel, titled Forms Tree, to help navigate structure of Headless adaptive form. 

-->

## Voraussetzungen

* Laden Sie [Microsoft Visual Studio Code 1.62.0 oder höher](https://code.visualstudio.com/docs/supporting/FAQ#_how-do-i-find-the-version) herunter und installieren Sie es. Wenn Sie eine ältere Version oder bisher keine Version installiert haben, laden Sie die neueste Version von der [Microsoft-Website](https://code.visualstudio.com/docs/setup/setup-overview) herunter. Informationen zur Verwendung von Visual Studio über die Befehlszeile in Apple macOS finden Sie unter [Starten über die Befehlszeile](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line).
* Laden Sie die [Builder-Erweiterung für adaptive Formulare](/help/assets/adaptive-form-builder-0.12.0.vsix) herunter.

## Installieren der Erweiterung

1. Öffnen Sie die Eingabeaufforderung und navigieren Sie zu dem Verzeichnis, das die heruntergeladene Erweiterungsdatei *adaptive-form-builder-[version].vsix* enthält.

1. Führen Sie den folgenden Befehl aus, um die Erweiterung zu installieren:

   `code -–install-extension adaptive-form-builder-0.12.0.vsix`

   <br>

   ![Installieren der Erweiterung](/help/assets/install-extension.png)


   Weitere Informationen zu VSIX-Dateien finden Sie in der [Hilfe zu Microsoft Visual Studio Code](https://code.visualstudio.com/docs/editor/extension-marketplace#_install-from-a-vsix).
