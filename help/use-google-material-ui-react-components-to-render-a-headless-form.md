---
title: Rendern eines Headless-Formulars mithilfe der React-Komponenten der Google Material-Benutzeroberfläche
description: Erfahren Sie, wie Sie mit den React-Komponenten der Google Material-Benutzeroberfläche ein Headless-Formular rendern können. Diese umfassende Anleitung führt Sie schrittweise durch die Erstellung von Komponenten für benutzerdefinierte adaptive Headless-Formulare und zeigt Ihnen, wie Sie die React-Komponenten der Google Material-Benutzeroberfläche nutzen, um ein adaptives Headless-Formular zu formatieren.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
hide: false
exl-id: 476509d5-f4c1-4d1c-b124-4c278f67b1ef
source-git-commit: 47ac7d03c8c4fa18ac3bdcef04352fdd1cad1b16
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Verwenden einer benutzerdefinierten React-Bibliothek zum Rendern eines Headless-Formulars

Sie können benutzerdefinierte Komponenten erstellen und implementieren, um das Erscheinungsbild und die Funktionalität (Verhalten) Ihrer adaptiven Headless-Formulare gemäß den Anforderungen und Richtlinien Ihres Unternehmens anzupassen.

Diese Komponenten dienen hauptsächlich dazu, das Erscheinungsbild oder den Stil von Formularfeldern festzulegen und die über diese Felder erfassten Daten in der Formularmodellinstanz zu speichern. Wenn das verwirrend klingt, machen Sie sich keine Sorgen – wir werden diese Aspekte in Kürze genauer untersuchen. Zunächst konzentrieren wir uns auf die ersten Schritte zur Erstellung benutzerdefinierter Komponenten, zum Rendern des Formulars mit diesen Komponenten und zur Verwendung von Ereignissen zum Speichern und Senden von Daten an einen REST-Endpunkt.

In diesem Tutorial wird anhand von Komponenten der Google Material-Benutzeroberfläche demonstriert, wie ein adaptives Headless-Formular mit benutzerdefinierten React-Komponenten wiedergegeben wird. Sie sind jedoch nicht auf diese Bibliothek beschränkt und können jede React-Komponentenbibliothek nutzen oder eigene benutzerdefinierte Komponenten entwickeln.

Am Ende dieses Artikels verwandelt sich das _Kontakt_-Formular, das im Artikel [Erstellen und Veröffentlichen eines Headless-Formulars mit dem Starterkit](create-and-publish-a-headless-form.md) erstellt wurde, in Folgendes:

![](assets/headless-adaptive-form-with-google-material-ui-components.png)


Die wichtigsten Schritte beim Rendern eines Formulars mit den Komponenten der Google Material-Benutzeroberfläche:

![](assets/headless-forms-graphics-source-main.svg)

## 1. Installieren der Google Material-Benutzeroberfläche

Standardmäßig verwendet das Starterkit [Adobe Spectrum](https://spectrum.adobe.com/)-Komponenten. Konfigurieren wir sie für die Verwendung der [Google Material-Benutzeroberfläche](https://mui.com/):

1. Stellen Sie sicher, dass das Starterkit nicht ausgeführt wird. Um das Starterkit zu stoppen, öffnen Sie das Terminal, navigieren Sie zu **react-starter-kit-aem-headless-forms** und drücken Sie Strg-C (unter Windows, Mac und Linux identisch).

   Versuchen Sie nicht, das Terminal zu schließen. Durch Schließen Ihres Terminals wird das Starterkit nicht gestoppt.

1. Führen Sie den folgenden Befehl aus:

```shell
    
    npm install @mui/material @emotion/react @emotion/styled --force
    
```

Dadurch werden die npm-Bibliotheken der Google Material-Benutzeroberfläche installiert und zu den Abhängigkeiten des Starterkits hinzugefügt. Sie können Formularkomponenten jetzt mit den Komponenten der Material-Benutzeroberfläche rendern.


## 2. Erstellen benutzerdefinierter React-Komponenten

Erstellen wir eine benutzerdefinierte Komponente, die die Standardkomponente [Texteingabe](https://spectrum.adobe.com/page/text-field/) durch die Komponente [Textfeld der Google Material-Benutzeroberfläche](https://mui.com/material-ui/react-text-field/) ersetzt.

Für jeden Komponententyp ist eine separate Komponente erforderlich ([fieldType](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-json-properties-fieldtype--text-input) oder :type), die in einer Definition für Headless-Formulare verwendet wird. Beispielsweise sind im Kontaktformular, das Sie im vorherigen Abschnitt erstellt haben, die Felder Name, E-Mail und Telefon vom Typ `text-input` ([fieldType: &quot;text-input&quot;](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/docs/adaptive-form-components-text-input-field--def)) und das Meldungsfeld vom Typ `multiline-input` ([&quot;fieldType&quot;: &quot;multiline-input&quot;](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/docs/reference-json-properties-fieldtype--multiline-input)).


Erstellen wir eine benutzerdefinierte Komponente, um alle Formularfelder zu überlagern, die die Eigenschaft [fieldType: &quot;text-input&quot;](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/docs/adaptive-form-components-text-input-field--def) mit der Komponente [Textfeld der Material-Benutzeroberfläche](https://mui.com/material-ui/react-text-field/) verwenden.


So erstellen Sie die benutzerdefinierten Komponente und ordnen sie der Eigenschaft [fieldType](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/docs/adaptive-form-components-text-input-field--def) zu:

1. Öffnen Sie das Verzeichnis **react-starter-kit-aem-headless-forms** in einem Code-Editor und navigieren Sie zu `\react-starter-kit-aem-headless-forms\src\components`.


1. Erstellen Sie eine Kopie des Ordners **Slider** oder **Richtext** und benennen Sie den kopierten Ordner um in **materialtextfield**. Slider und RichText sind zwei benutzerdefinierte Beispielkomponenten, die in der Starter-App verfügbar sind. Sie können diese verwenden, um eigene benutzerdefinierte Komponenten zu erstellen.

   ![Die benutzerdefinierte Komponente „materialtextfield“ in VSCode](/help/assets/richtext-custom-component-in-vscode.png)

1. Öffnen Sie die Datei `\react-starter-kit-aem-headless-forms\src\components\materialtextfield\index.tsx` und ersetzen Sie den vorhandenen Code durch folgenden Code. Dieser Code gibt eine Komponente [Textfeld der Google Material-Benutzeroberfläche](https://mui.com/material-ui/react-text-field/) zurück und rendert sie

```JavaScript
 
     import React from 'react';
     import {useRuleEngine} from '@aemforms/af-react-renderer';
     import {FieldJson, State} from '@aemforms/af-core';
     import { TextField } from '@mui/material';
     import Box from '@mui/material/Box';
     import { richTextString } from '@aemforms/af-react-components';
     import Typography from '@mui/material/Typography';


     const MaterialtextField = function (props: State<FieldJson>) {

         const [state, handlers] = useRuleEngine(props);

         return(

         <Box>
             <Typography component="legend">{state.visible ? richTextString(state?.label?.value): ""} </Typography>
             <TextField variant="filled"/>
         </Box>

         )
     }

     export default MaterialtextField;
```


Der Teil `state.visible` überprüft, ob die Komponente als sichtbar festgelegt ist. Ist dies der Fall, wird die Feldbeschriftung abgerufen und mit `richTextString(state?.label?.value)` angezeigt.

![](/help/assets/material-text-field.png)


Ihre benutzerdefinierte Komponente `materialtextfield` ist bereit. Legen wir diese benutzerdefinierte Komponente fest, um alle Instanzen von [fieldType: &quot;text-input&quot;](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/docs/adaptive-form-components-text-input-field--def) durch „Textfeld der Google Material-Benutzeroberfläche“ zu ersetzen.

## 3. Ordnen Sie Headless-Formularfeldern benutzerdefinierten Komponenten zu

Das Rendern von Formularfeldern mithilfe von Komponenten aus Drittanbieterbibliotheken wird als Zuordnung bezeichnet. Dabei ordnen Sie jeden ([fieldType](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-json-properties-fieldtype--text-input)) der entsprechenden Komponente der Drittanbieterbibliothek zu.

Alle zuordnungsbezogenen Informationen werden zur Datei `mappings.ts` hinzugefügt. Die `...mappings`-Anweisung in der Datei `mappings.ts` bezieht sich auf die Standardzuordnungen, die den ([fieldType](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-json-properties-fieldtype--text-input) oder :type) mit [Adobe Spectrum](https://spectrum.adobe.com/page/text-field/)-Komponenten überlagern.

So ordnen Sie die im letzten Schritt erstellte `materialtextfield`-Komponente zu:

1. Öffnen Sie die Datei `mappings.ts`.

1. Fügen Sie folgende Importanweisung hinzu, um die Komponente `materialtextfield` in die Datei `mappings.ts` einzuschließen.


   ```JavaScript
       import MaterialtextField from "../components/materialtextfield";
   ```

1. Fügen Sie folgende Anweisung hinzu, um den `text-input` der Komponente „materialtextfield“ zuzuordnen.


   ```JavaScript
       "text-input": MaterialtextField
   ```

   Der endgültige Code der Datei sieht wie folgt aus:

   ```JavaScript
         import { mappings } from "@aemforms/af-react-components";
         import MaterialtextField from "../components/materialtextfield";
   
   
         const customMappings: any = {
           ...mappings,
           "text-input": MaterialtextField
        };
        export default customMappings;
   ```

1. Speichern Sie die App und führen Sie sie aus. Die ersten drei Felder des Formulars werden mithilfe des [Textfelds der Google Material-Benutzeroberfläche](https://mui.com/material-ui/react-text-field/) erstellt:

   ![](assets/material-text-field-form-rendetion.png)


   Auf ähnliche Weise können Sie benutzerdefinierte Komponenten für die Felder „Meldung“ (&quot;fieldType&quot;: &quot;multiline-input&quot;) erstellen und die Dienstfelder (&quot;fieldType&quot;:&quot;number-input&quot;) bewerten. Sie können folgendes Git-Repository für benutzerdefinierte Komponenten der Nachricht klonen und die Dienstfelder bewerten:

   [https://github.com/singhkh/react-starter-kit-aem-headless-forms](https://github.com/singhkh/react-starter-kit-aem-headless-forms)

## Nächster Schritt

Sie haben das Formular erfolgreich mit benutzerdefinierten Komponenten, die die Google Material-Benutzeroberfläche verwenden, gerendert. Haben Sie versucht, das Formular zu senden, indem Sie auf die Schaltfläche „Senden“ geklickt haben (der entsprechenden Komponente der Google Material-Benutzeroberfläche zugeordnet)? Wenn nicht, versuchen Sie es.

Sendet das Formular die Daten an eine Datenquelle? Nein? Machen Sie sich keine Sorgen. Dies liegt daran, dass Ihr Formular nicht für die Kommunikation mit der Laufzeitbibliothek konfiguriert ist.

Wie können Sie Ihr Formular so konfigurieren, dass es mit ihr kommuniziert? Wir veröffentlichen bald einen Artikel, der alles im Detail erklärt. Bleiben Sie dran!
