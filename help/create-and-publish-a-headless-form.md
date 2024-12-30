---
title: Erstellen und Veröffentlichen eines Headless-Formulars mit Adobe Experience Manager Adaptive Forms | Schrittweise Anleitung
description: In dieser schrittweisen Anleitung erfahren Sie, wie Sie ein Headless-Formular mit den adaptiven Formularen von Adobe Experience Manager erstellen und veröffentlichen. Erfahren Sie mehr über die Vorteile des Headless-Modus und die Optimierung der Formularerstellung. Beginnen Sie mit dem Erstellen dynamischer, responsiver Formulare mit adaptiven Headless-Formularen von Adobe Experience Manager, die geräteübergreifend nahtlos funktionieren.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
hide: false
exl-id: cd7c7972-376c-489f-a684-f479d92c37e7
source-git-commit: 47ac7d03c8c4fa18ac3bdcef04352fdd1cad1b16
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---



# Erstellen und Anzeigen einer Vorschau eines Headless-Formulars mit einer React-App {#introduction}

Das Starterkit hilft Ihnen bei den ersten Schritten mit einer React-App. Sie können adaptive Headless-Formulare in einer Angular-, Vanilla JS- und anderen Entwicklungsumgebungen Ihrer Wahl entwickeln und verwenden.

Der Einstieg in adaptive Headless-Formulare ist ziemlich einfach und schnell. Klonen Sie das fertige React-Projekt, installieren Sie die Abhängigkeiten und führen Sie das Projekt aus. Sie verfügen über ein adaptives Headless-Formular, das in eine React-App integriert ist. Sie können das React-Beispielprojekt verwenden, um adaptive Headless-Formulare zu erstellen und zu testen, bevor Sie diese in einer Produktionsumgebung bereitstellen.

Fangen wir an:

>[!NOTE]
>
>
> In diesem Erste-Schritte-Handbuch wird eine React-App verwendet. Es steht Ihnen frei, Technologien oder Programmiersprachen Ihrer Wahl zu verwenden, um mit adaptiven Headless-Formularen zu arbeiten.

## Bevor Sie beginnen {#pre-requisites}

Um eine React-App zu erstellen und auszuführen, muss auf Ihrem Computer Folgendes installiert sein:

* Installieren Sie die [neueste Version von Git](https://git-scm.com/downloads). Wenn Sie mit Git noch nicht vertraut sind, lesen Sie [Git installieren](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

* Installieren Sie [Node.js 16.13.0 oder höher](https://nodejs.org/de/download/). Wenn Sie mit Node.js noch nicht vertraut sind, lesen Sie die [Installationsanleitung für Node.js](https://nodejs.dev/en/learn/how-to-install-nodejs).

## Erste Schritte

Nachdem die Anforderungen erfüllt sind, führen Sie die folgenden Schritte aus, um zu beginnen:

1. [Einrichten des Starterkits für adaptive Headless-Formulare](#setup)

1. [Anzeigen einer Vorschau des adaptiven Headless-Formulars im Starterkit](#preview)

1. [Erstellen und Rendern eines eigenen adaptiven Headless-Formulars](#custom)



## 1. Einrichten des Starterkits für adaptive Headless-Formulare {#install}

Das Starterkit ist eine React-App mit einem adaptiven Headless-Beispielformular und entsprechenden Bibliotheken. Verwenden Sie das Kit, um Ihre adaptiven Headless-Formulare und entsprechenden React-Komponenten zu entwickeln und zu testen. Führen Sie die folgenden Befehle aus, um das Starterkit für adaptive Headless-Formulare einzurichten:

1. Öffnen Sie eine Eingabeaufforderung und führen Sie den folgenden Befehl aus:

   ```shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   Der Befehl erstellt ein Verzeichnis mit dem Namen **react-starter-kit-aem-headless-forms** an Ihrem aktuellen Speicherort und klont die React-Starter-App für adaptive Headless-Formulare. Zusammen mit den Konfigurationen und der Liste der Abhängigkeiten, die zum Rendern des Formulars erforderlich sind, enthält der Ordner die folgenden wichtigen Inhalte:

   * **Beispielformular**: Das Starterkit enthält ein Beispielformular für einen Darlehensantrag. Um das in der App enthaltene Formular (Formulardefinition) anzuzeigen, öffnen Sie die Datei `/react-starter-kit-aem-headless-forms/form-definations/form-model.json`.
   * **React-Beispielkomponenten**: Das Starterkit enthält React-Beispielkomponenten für Rich Text und Slider. Dieses Handbuch hilft Ihnen beim Erstellen eigener benutzerdefinierter Komponenten mit diesen Rich-Text- und Slider-Komponenten.
   * **Mappings.ts**: Mithilfe der Datei „mappings.ts“ können Sie benutzerdefinierte Komponenten Formularfeldern zuordnen. Sie können beispielsweise ein numerisches Schrittfeld der Bewertungskomponente zuordnen.
   * **Umgebungskonfigurationen**: Mit Umgebungskonfigurationen können Sie ein im Starterkit enthaltenes Formular wiedergeben oder ein Formular von einem AEM Forms-Server abrufen.

   ![](/help/assets/getting-started-starter-kit-content.png)

   >[!NOTE]
   >
   > 
   > Beispiele in Dokumenten basieren auf VSCode. Sie können auch einen beliebigen einfachen Texteditor für Code verwenden.


1. Navigieren Sie zum Verzeichnis **react-starter-kit-aem-headless-forms** und führen Sie den folgenden Befehl aus, um die Abhängigkeiten zu installieren:

   ```shell
   npm install
   ```

   Der Befehl lädt alle Pakete und Bibliotheken herunter, die zum Ausführen und Erstellen der App erforderlich sind, z. B. Bibliotheken für adaptive Headless-Formulare
(@aemforms/af-response-renderer, @aemforms/af-response-components, @adobe/react-frequency), führt Validierungen durch und persistiert Daten für Instanzen des Formulars.

   ![](/help/assets/install-react-app-starter-kit.png)


## 2. Anzeigen des adaptiven Headless-Formulars in der Vorschau {#preview}

Nachdem Sie das Starterkit eingerichtet haben, können Sie eine Vorschau des adaptiven Headless-Beispielformulars anzeigen und es durch Ihr eigenes, benutzerdefiniertes Formular ersetzen. Sie können auch das Starterkit konfigurieren, um ein Formular von einem AEM Forms-Server abzurufen. So zeigen Sie eine Vorschau des Formulars an

1. Benennen Sie die Datei `env_template` in `.env` um. Stellen Sie außerdem sicher, dass die Option USE_LOCAL_JSON auf „true“ gesetzt ist.

   ![](/help/assets/rename-env-file.png)

   <!-- The options in the .env file help you configure source of the forms definantion (.JSON):
    *  To source forms definantion (.JSON) from an AEM Server, set USE_LOCAL_JSON option to false, use the AEM_URL option to specify URL  of your AEM Server, and set the AEM_FORM_PATH option to path of your adaptive form.
    *  To source forms definantion (.JSON) form-model.json file included in the starter-kit, set USE_LOCAL_JSON option to false. -->

1. Verwenden Sie den folgenden Befehl, um die App auszuführen:

   ```shell
     npm start
   ```


   Mit diesem Befehl wird ein lokaler Entwicklungs-Server gestartet, und das in der Starter App enthaltene adaptive Headless-Beispielformular wird in Ihrem Standard-Webbrowser geöffnet.

   ![Headless-Beispielformular](assets/sample-headless-adaptive-form.png)

   Und fertig! Jetzt ist alles so eingerichtet, dass Sie mit der Entwicklung eines benutzerdefinierten adaptiven Headless-Formulars beginnen können.

   <!--  As you know, in a headless form the form data and logic are separate from the presentation layer and can be used by any client that can make HTTP requests, such as a mobile app, a static site, or a different web application. The form is often managed and stored on a server, which serves as the backend for the form. The client sends requests to the server to retrieve the form, submit data, and receive updated form data. This allows for greater flexibility and integration with different technologies. You can store and retrive a Headless adaptive form on an AEM Server  -->

## 3. Erstellen und Rendern eines eigenen adaptiven Headless-Formulars{#custom}

Ein adaptives Headless-Formular stellt das Formular und seine Komponenten, wie Felder und Schaltflächen, im JSON-Format (JavaScript Object Notation) dar. Der Vorteil der Verwendung des JSON-Formats besteht darin, dass es von verschiedenen Programmiersprachen einfach analysiert und verwendet werden kann, sodass Formulardaten bequem zwischen Systemen ausgetauscht werden können. Um das in der App enthaltene adaptive Headless-Beispielformular anzuzeigen, öffnen Sie die Datei `/react-starter-kit-aem-headless-forms/form-definations/form-model.json`.

Erstellen wir ein Kontaktformular mit vier Feldern: „Name“, „E-Mail“, „Kontaktnummer“und „Nachricht“. Die Felder werden als Objekte (Elemente) innerhalb der JSON-Datei definiert, wobei jedes Objekt (Element) Eigenschaften aufweist, wie „Typ“, „Bezeichnung“, „Name“ und „Erforderlich“. Das Formular verfügt auch über eine Schaltfläche vom Typ „Übermitteln“. Hier finden Sie die JSON für das Formular.


```JSON
{
  "afModelDefinition": {
    "adaptiveform": "0.10.0",
    "items": [
      {
        "fieldType": "text-input",
        "label": {
          "value": "Name"
        },
        "name": "name"
      },
      {
        "fieldType": "text-input",
        "format": "email",
        "label": {
          "value": "Email"
        },
        "name": "email"
      },
      {
        "fieldType": "text-input",
        "format": "phone",
        "pattern": "[0-9]{10}",
        "label": {
          "value": "Contact Number"
        },
        "name": "Phone"
      },
      {
        "fieldType": "multiline-input",
        "label": {
          "value":"Message"
        },
        "name": "message"
      },
      {
        "fieldType": "button",
        "label":{
          "value": "Submit"
        },
        "name":"submit",
        "events":{
          "click": "submitForm()"
        }
      }
    ],
    "action": "https://eozrmb1rwsmofct.m.pipedream.net",
    "description": "Contact Us",
    "title": "Contact Us",
    "metadata": {
      "grammar": "json-formula-1.0.0",
      "version": "1.0.0"
    }
  }
}
```

>[!NOTE]
>
> * Das Attribut „afModelDefinition“ ist nur für React-Apps erforderlich und ist nicht Teil der Formulardefinition.
> * Sie können die JSON für das Formular manuell erstellen oder den [AEM-Editor für adaptive Formulare (WYSIWYG-Editor für adaptive Formulare)](create-a-headless-adaptive-form.md) verwenden, um die Formular-JSON zu erstellen und bereitzustellen. In einer Produktionsumgebung verwenden Sie AEM Forms, um die Formular-JSON bereitzustellen, mehr dazu später.
> * In diesem Tutorial wird „https://pipedream.com/“ zum Testen der Formularübermittlung verwendet. Sie verwenden Ihre eigenen Endpunkte oder Drittanbieter-Endpunkte, die von Ihrer Organisation genehmigt wurden, um die Daten aus einem adaptiven Headless-Formular zu empfangen.


Um das Formular zu rendern, ersetzen Sie die JSON-Musterdatei für das adaptive Headless-Formular `/react-starter-kit-aem-headless-forms/form-definations/form-model.json` durch die obige JSON, speichern Sie die Datei und warten Sie, bis das Starterkit das Formular kompiliert und aktualisiert hat.

![Ersetzen Sie die JSON-Datei für das adaptive Headless-Beispielformular `/react-starter-kit-aem-headless-forms/form-definations/form-model.json` durch die JSON für das benutzerdefinierte adaptive Headless-Formular](assets/render-custom-headless-adaptive-form.png)

<!-- Your form is ready. Let's add some validations and make "Name", "Email", and "Message" fields mandatory. -->

Sie haben das adaptive Headless-Formular erfolgreich gerendert.


## Bonus

Legen wir den Titel der Web-Seite, die das Formular hostet, auf `Contact Us | WKND Adventures and Travel` fest. Um den Titel zu ändern, öffnen Sie die Datei _react-starter-kit-aem-headless-forms/public/index.html_ zur Bearbeitung und legen Sie den Titel fest.

![](assets/contact-us-headless-adaptive-forms-updated-title.png)


## Nächster Schritt

Standardmäßig verwendet das Starterkit [Adobe](https://spectrum.adobe.com/)-Komponenten zum Rendern des Formulars. Sie können Ihre eigenen Komponenten erstellen und verwenden oder auch Drittanbieterkomponenten. Beispielsweise die Google Material-Benutzeroberfläche oder die Chakra-Benutzeroberfläche.

Nutzen wir die [Google Material-Benutzeroberfläche](use-google-material-ui-react-components-to-render-a-headless-form.md), um unser Kontaktformular zu rendern.




