---
title: Erstellen des ersten adaptiven Headless-Formulars
description: Erstellen des ersten adaptiven Headless-Formulars
keywords: Headless, adaptives Formular
hide: true
exl-id: 99985fed-4a34-47d6-bb6f-79f81e1cd71b
source-git-commit: 41286ff4303e0f4d404deb113fd59d1499768da5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Erstellen Ihres ersten adaptiven Headless-Formulars

Sie können Headless-Formulare von Adobe Experience Manager verwenden, um Formularanwendungen mithilfe von Frontend-UI-Frameworks wie React zu erstellen, und das Forms Web SDK für Funktionen wie Statusverwaltung, Validierung und Integrationen mit verschiedenen anderen Touchpoints verwenden.

Beispiel: Das Unternehmen We.Org möchte die Journey seiner Kundenanmeldung digitalisieren. Sein Entwicklungs-Team ist mit der Verwendung von Angular zum Erstellen von Frontend-Lösungen sehr vertraut. Das Unternehmen möchte ein benutzerdefiniertes Frontend erstellen, während es die Formularüberprüfung und elektronische Signaturen in spezielle Lösungen auslagert.

Adaptive Headless-Formulare von Adobe Experience Manager bieten Unternehmen die Möglichkeit, Formulare mithilfe ihres vorhandenen Know-hows in Frontend-Sprachen zu erstellen. Gleichzeitig bieten sie Unterstützung für die Verwendung von Backend-Funktionen, um ein Formularerlebnis der Unternehmensklasse zu schaffen.

<!-- >>[!VIDEO](https://video.tv.adobe.com/v/341011/) -->

<!--  ![Create a Headless adaptive form](/help/assets/headless-forms.png) -->

## Bevor Sie beginnen

* Richten Sie die [Entwicklungsumgebung](setup-development-environment.md) ein, damit Sie ein adaptives Headless-Formular auf Ihrem lokalen Computer erstellen und testen können.
* Die folgende Software muss auf Ihrem lokalen Entwicklungscomputer installiert sein:
   * [Java Development Kit 11](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&amp;1_group.propertyvalues.operation=equals&amp;1_group.propertyvalues.0_values=software-type%3Atooling&amp;fulltext=Oracle%7E+JDK%7E+11%7E&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=14)
   * [Die neueste Version von Git](https://git-scm.com/downloads). Wenn Sie mit Git noch nicht vertraut sind, lesen Sie [Installieren von Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
   * [Node.js 16.13.0 oder höher](https://nodejs.org/de/download/). Wenn Sie mit Node.js noch nicht vertraut sind, lesen Sie die [Installationsanleitung für Node.js](https://nodejs.dev/en/learn/how-to-install-nodejs).
   * [Maven 3.6 oder höher](https://maven.apache.org/download.cgi). Wenn Sie mit Maven noch nicht vertraut sind, lesen Sie [Installieren von Apache Maven](https://maven.apache.org/install.html).


## Verwenden des Archetyp-Projekts zum Erstellen eines adaptiven Headless-Formulars

Das Archetyp-Projekt ist eine Maven-basierte Vorlage. Es wird ein minimales Projekt basierend auf Best Practices erstellt, um mit adaptiven Headless-Formularen zu beginnen. Es enthält auch Funktionen für adaptive Headless-Formulare für Forms as a Cloud Service und lokale Entwicklungsumgebungen. Es ist erforderlich, das auf dem Archetyp 37 oder höher basierende Projekt während der Betaphase zu erstellen und bereitzustellen. Nach der Betaphase ist das Projekt nur für Anpassungen erforderlich.

Führen Sie die folgenden Schritte aus, um Ihr erstes adaptives Headless-Formular zu erstellen und zu rendern:

1. [Erstellen und Bereitstellen eines auf einem Archetyp basierenden Projekts von AEM](#create-an-archetype-based-project)
1. [Bereitstellen des Projekts für das AEM SDK](#deploy-the-project-to-a-local-development-environment)
1. [Erstellen des JSON-Schemas des adaptiven Headless-Formulars und Hochladen in Ihre AEM SDK-Instanz](#create-add-json-representation-of-headless-adaptive-forms)
1. [Erstellen eines adaptiven Formulars basierend auf der Vorlage „Leer mit Kernkomponenten“](#create-adaptive-form-with-blank-with-core-components-template)


### 1. Erstellen und Bereitstellen eines auf einem Archetyp basierenden Projekts von AEM {#create-an-archetype-based-project}

Führen Sie je nach Betriebssystem den folgenden Befehl aus, um ein Experience Manager Forms as a Cloud Service-Projekt zu erstellen. Verwenden Sie den Archetyp Version 37 oder höher. Siehe [Archetyp-Dokumentation](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=de), um die neueste Version des Archetyps zu finden.

**Microsoft Windows**

1. Öffnen Sie die Eingabeaufforderung mit Administratorrechten (Führen Sie die Eingabeaufforderung oder die Bash-Shell als Admin aus)
1. Führen Sie den folgenden Befehl aus:

   ```shell
     mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
     -D archetypeGroupId=com.adobe.aem ^
     -D archetypeArtifactId=aem-project-archetype ^
     -D archetypeVersion=37 ^
     -D appTitle=myheadlessform ^
     -D appId=myheadlessform ^
     -D groupId=com.myheadlessform ^
     -D includeFormsenrollment="y" ^
     -D includeFormsheadless="y" 
   ```

   * Passen Sie `appTitle` an, um den Titel und die Komponentengruppen festzulegen.
   * Passen Sie `appId` an, um die Maven-Artefakt-ID (artifactId), die Namen der Komponenten-, Konfigurations- und Inhaltsordner sowie die Namen der Client-Bibliotheken festzulegen.
   * Passen Sie `groupId` an, um die Maven-Gruppen-ID (groupId) und das Java-Quellpaket festzulegen.
   * Verwenden Sie die Option `includeFormsenrollment=y` zum Einschließen von Forms-spezifischen Konfigurationen, Designs, Vorlagen, Kernkomponenten und Abhängigkeiten, die zum Erstellen adaptiver Formulare erforderlich sind.
   * Durch Verwenden der Option `includeFormsheadless=y` werden Formular-Kernkomponenten und -Abhängigkeiten einbezogen, die für die Verwendung der Funktion für adaptive Headless-Formulare erforderlich sind. Wenn Sie diese Option aktivieren, sind folgende Punkte enthalten:
      * Die Vorlage **Leer mit Kernkomponenten** mit [Kernkomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=de).
      * Ein Frontend-React-Modul, `ui.frontend.react.forms.af`. Es hilft Ihnen, das adaptive Headless-Formular in einer React-App zu rendern.


**Apple macOS oder Linux**:

1. Öffnen Sie das Terminal als Root-Benutzerin bzw. -Benutzer. So können Sie Befehle mit Administratorrechten ausführen. Sie können nach dem Öffnen des Terminalfensters, um Befehle mit Administratorrechten auszuführen, auch den Befehl `sudo root` verwenden.
1. Führen Sie den folgenden Befehl aus:

   ```shell
     mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
     -D archetypeGroupId=com.adobe.aem \
     -D archetypeArtifactId=aem-project-archetype \
     -D archetypeVersion=37 \
     -D appTitle=myheadlessform \
     -D appId=myheadlessform \
     -D groupId=com.myheadlessform \
     -D includeFormsenrollment="y" \
     -D includeFormsheadless="y"  
   ```

   * Passen Sie `appTitle` an, um den Titel und die Komponentengruppen festzulegen.
   * Passen Sie `appId` an, um die Maven-Artefakt-ID (artifactId), die Namen der Komponenten-, Konfigurations- und Inhaltsordner sowie die Namen der Client-Bibliotheken festzulegen.
   * Passen Sie `groupId` an, um die Maven-Gruppen-ID (groupId) und das Java-Quellpaket festzulegen.
   * Verwenden Sie die Option `includeFormsenrollment=y` zum Einschließen von Forms-spezifischen Konfigurationen, Designs, Vorlagen, Kernkomponenten und Abhängigkeiten, die zum Erstellen adaptiver Formulare erforderlich sind.
   * Durch Verwenden der Option `includeFormsheadless=y` werden Formular-Kernkomponenten und -Abhängigkeiten einbezogen, die für die Verwendung der Funktion für adaptive Headless-Formulare erforderlich sind. Wenn Sie diese Option aktivieren, sind folgende Punkte enthalten:
      * Die Vorlage **Leer mit Kernkomponenten** mit [Kernkomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=de).
      * Ein Frontend-React-Modul, `ui.frontend.react.forms.af`. Es hilft Ihnen, das adaptive Headless-Formular in einer React-App zu rendern.

Nach erfolgreichem Abschluss des Befehls wird ein Projektordner mit dem im `appID` angegebenen Namen erstellt. Wenn Sie beispielsweise `appID` mit dem Wert `myheadlessform` verwenden, wird ein Ordner mit dem Namen `myheadlessform` erstellt. Er enthält das auf dem Archetyp basierende Projekt.


### 2. Bereitstellen des Projekts für das AEM SDK {#deploy-the-project-to-a-local-development-environment}

Wenn Sie das Projekt in Ihrer AEM SDK-Instanz bereitstellen, werden die Funktion für adaptive Headless-Formulare, die Vorlage **Leer mit Kernkomponenten** und andere Ressourcen, die im Projekt enthalten sind, zu Ihrer Entwicklungsumgebung hinzugefügt. <!-- Deploy the project to your local development environment to locally create Headless Adaptive Forms. or deploy directly to your Forms as a Cloud Service environment. !--> So stellen Sie Ihre AEM SDK-Instanz bereit:

1. Öffnen Sie eine Eingabeaufforderung. Wenn Sie mit Windows arbeiten, öffnen Sie die Eingabeaufforderung mit Administratorrechten (Eingabeaufforderung oder [Git-Bash-Shell](https://khushwantsehgal.wordpress.com/2022/06/29/check-if-git-bash-is-running-in-administrator-mode/) als Admin ausführen).

1. Navigieren Sie zum Projektverzeichnis, das im vorherigen Schritt erstellt wurde. Zum Beispiel: `/myheadlessform`

   ![Projektverzeichnis](assets/project-directory.png)

1. Führen Sie den folgenden Befehl aus:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   Warten Sie auf die Meldung „BUILD SUCCESS“.
   ![Projekt erfolgreich bereitgestellt](assets/project-deployed-successfully.png)

   Es kann lange dauern, die Dateiabhängigkeiten zu beheben und das Projekt bereitzustellen. Wenn die Bereitstellung des Projekts fehlschlägt, lesen Sie den Artikel zur [Fehlerbehebung](troubleshooting.md). Dort finden Sie häufige Probleme und deren Lösung.


<!-- *  To learn how to deploy code to AEM as a Cloud Service, see the video in [Deploying to AEM as a Cloud Service]https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en#coding-against-the-right-aem-version) article : -->


### 3. Erstellen des JSON-Schemas des adaptiven Headless-Formulars und Hochladen in Ihre AEM SDK-Instanz {#create-add-json-representation-of-headless-adaptive-forms}

Ein adaptives Headless-Formular wird als JSON-Datei dargestellt. Sie können ein Beispielformular aus [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-examples--contact) abrufen oder die Beispielformulare aus dem Archetyp-Projekt unter `[Archetype Project]\ui.content\src\main\content\jcr_root\content\dam\myheadlessform\af_model_sample.json` verwenden. Dieses Dokument verwendet das Formular [Einführung](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-examples--introduction) aus dem Storybook. Es ist ein Formular mit einem einzelnen Feld, mit dem Sie schnell mit adaptiven Headless-Formularen beginnen können. <!-- The [specifications](/help/assets/Headless-Adaptive-Form-Specification.pdf) document provides detailed information about various components, rules, and constraints for Headless Adaptive Forms -->

So erstellen Sie das Schema und laden es hoch:

1. Erstellen Sie eine Nur-Text-Datei mit der Erweiterung `.json`. Beispiel: `myfirstform.json`. Sie können die Datei an einer beliebigen Stelle in Ihrem Dateisystem oder in Ihrem AEM Archetyp-basierten Projekt unter `\<project-name>\ui.content\src\main\content\jcr_root\content\dam\myheadlessform\<formname>.json` erstellen
1. Fügen Sie Ihrer `.json`-Datei folgenden Code hinzu und speichern Sie die Änderung:

   ```JSON
   {
     "adaptiveform": "0.10.0",
     "items": [
       {
         "fieldType": "text-input",
         "label": {
           "value": "Enter your Name"
         },
         "name": "textInput"
       }
     ],
     "metadata": {
       "grammar": "json-formula-1.0.0",
       "version": "1.0.0"
     }
   }
   ```

   Es wird ein einzelnes Feld zum Formular hinzugefügt:

   ![Hello World](assets/introduction.png)

1. Melden Sie sich bei Ihrer [lokalen AEM SDK-Instanz](setup-development-environment.md#setup-author-instance) an
1. Gehen Sie zu „Adobe Experience Manager“ > „Forms“ > „Formulare und Dokumente“. Tippen Sie auf „Erstellen“ > „Datei hochladen“.
1. Wählen Sie die in Schritt 2 erstellte `.json` aus und laden Sie sie hoch. Jetzt können Sie das adaptive Headless-Formular erstellen. Wenn Sie die JSON-Datei in Ihrem AEM Archetyp-basierten Projekt unter `\<project-name>\ui.content\src\main\content\jcr_root\content\dam\myheadlessform\<formname>.json` speichern, können Sie `mvn -PautoInstallPackage clean install` verwenden, um das Projekt mitsamt `<formname>.json` in Ihrem AEM SDK bereitzustellen.

Wenn beim Hochladen der `.json` ein Fehler auftritt, stellen Sie sicher, dass das [AEM-Archetyp-Projekt erfolgreich bereitgestellt wurde](#deploy-the-project-to-a-local-development-environment).

<!-- 1. Open the [contact form](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-examples--contact) and tap the [![Raw](assets/raw.png)](faq.md#storybook-example) icon on bottom-right side of the Storybook page to view the source code of the headless . 

You can use [Adaptive Forms builder extension for Visual Studio Code](/help/setup-development-environment.md#microsot-visual-studio-code-extension-for-headless-adaptive-forms) to build a JSON schema of your Headless Adaptive Forms. 

You can see [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-examples--introduction) for sample JSON schemas and list of components, attributes, and properties. You can also see the [specifications document](/help/assets/Headless-Adaptive-Form-Specification.pdf) for detailed information on all the components, constraints, and methods available to define Headless Adaptive Forms.

File extension of a JSON schema of Headless Adaptive Forms is .json. For example, formname.json. Create or add the file to your AEM Archetype based project. For example, `\myheadlessform\ui.content\src\main\content\jcr_root\content\dam\myheadlessform\home-loan.json` -> 

### 3. Deploy the project to a local development environment {#deploy-the-project-to-a-local-development-environment}

You can deploy the project to local development environment. It adds Headless Adaptive Forms functionality, the **Blank with core components** template, JSON schema of form, and other resources included in the project to your development environment. <!-- Deploy the project to your local development environment to locally create Headless Adaptive Forms. or deploy directly to your Forms as a Cloud Service environment. To deploy to your local development environment, use the following command: 

    `mvn -PautoInstallPackage clean install`

If you are on Windows, run the above with Administrative privileges (Run command prompt or [bash shell as an administrator](https://khushwantsehgal.wordpress.com/2022/06/29/check-if-git-bash-is-running-in-administrator-mode/)). For the complete list of commands, see [Building and Installing](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing).
    
<!-- *  To learn how to deploy code to AEM as a Cloud Service, see the video in [Deploying to AEM as a Cloud Service]https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en#coding-against-the-right-aem-version) article : -->

### 4. Erstellen eines adaptiven Formulars basierend auf der Vorlage „Leer mit Kernkomponenten“ {#create-adaptive-form-with-blank-with-core-components-template}

1. Melden Sie sich bei Ihrer [AEM SDK-Instanz](http://localhost:4502/) an.

1. Gehen Sie zu „Adobe Experience Manager“ > „Forms“ > „Formulare und Dokumente“.

1. Tippen Sie auf „Erstellen“ und wählen Sie „Adaptives Formular“. Wählen Sie die Vorlage **Leer mit Kernkomponenten** aus und tippen Sie auf „Erstellen“.

   ![Vorlage](assets/template.png)

1. Geben Sie die Werte für die folgenden Eigenschaftenfelder an. Die Felder „Titel“ und „Name“ sind obligatorisch.

   * **Titel:** Gibt den Anzeigenamen des Formulars an. Der Titel erleichtert Ihnen die Identifizierung des Formulars in der Benutzeroberfläche von Experience Manager Forms.
   * **Name:** Gibt den Namen des Formulars an. Im Repository wird ein Knoten mit dem angegebenen Namen erstellt. Wenn Sie mit der Eingabe des Titels beginnen, wird automatisch ein Wert für das Feld „Name“ vorgeschlagen. Sie können den vorgeschlagenen Wert gegebenenfalls ändern. Im Feld „Name“ dürfen nur alphanumerische Zeichen, Bindestriche und Unterstriche eingegeben werden. Alle ungültigen Eingaben werden durch Bindestriche ersetzt.

1. Tippen Sie auf „Erstellen“. Ein adaptives Formular wird erstellt.

Wenn die Vorlage **Leer mit Kernkomponenten** nicht angezeigt wird, stellen Sie sicher, dass das [AEM-Archetyp-Projekt erfolgreich bereitgestellt wurde](#deploy-the-project-to-a-local-development-environment).

### 5. Konfigurieren des adaptiven Formulars für die Verwendung des JSON-Schemas {#configure-adaptive-form-to-use-the-JSON-representation}

Das im vorherigen Schritt erstellte adaptive Formular ist leer. Konfigurieren Sie das adaptive Formular für die Verwendung des JSON-Schemas:

1. Melden Sie sich bei Ihrer [AEM SDK-Instanz](http://localhost:4502/) an.

1. Gehen Sie zu „Adobe Experience Manager“ > „Forms“ > „Formulare und Dokumente“. Wählen Sie das im vorherigen Schritt erstellte adaptive Formular aus und tippen Sie auf „Bearbeiten“. Das adaptive Formular wird im Editor geöffnet.

1. Tippen Sie auf die Komponente „Adaptive Formulare – Container“ und dann auf „Eigenschaften“. Der Eigenschaften-Explorer wird in der Seitenleiste angezeigt.

1. Erweitern Sie im Eigenschaften-Explorer das Akkordeon EINFACH und geben Sie den Pfad des in einem vorherigen Schritt hochgeladenen JSON-Schemas als Pfad zum Formular-Laufzeitdokument an. Die Container-Komponente zeigt eine Ausgabedarstellung des Formulars an.

1. Erweitern Sie im Eigenschaften-Explorer das Akkordeon ÜBERMITTLUNG und legen Sie eine Übermittlungsaktion für das adaptive Formular fest. Ihr Formular kann jetzt in einer React-App verwendet werden.

1. So rendern Sie das Formular auf Ihrem lokalen Entwicklungs-Computer:

   1. Öffnen Sie die Datei `[Archetype project]\ui.frontend.react.forms.af\.env` und legen Sie den Pfad des Formulars fest. Beispiel: /content/forms/af/contact

   1. Öffnen Sie die Eingabeaufforderung, navigieren Sie zum Projekt „ui.frontend.react.forms.af“ und führen Sie den folgenden Befehl aus:

      `npm run start`

   1. Öffnen Sie nach Abschluss „localhost:3000“ in Ihrem Browser-Fenster, um das gerenderte adaptive Headless-Formular anzuzeigen.
   1. Um die Übermittlungsfunktion zu testen, melden Sie sich bei Ihrem AEM Forms-Server an und verwenden Sie die Option **HTML-Vorschau** des Formulars, um das Formular im Vorschaumodus zu öffnen.

Das [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/) bietet eine Liste von Komponenten und Regeln, die für verschiedene adaptive Headless-Formulare festgelegt werden können, sowie ein Beispiel für ein JSON-Schema von adaptiven Headless-Formularen. Sie können auch das Dokument [Spezifikationen](/help/assets/Headless-Adaptive-Form-Specification.pdf) lesen, um mehr über verschiedene Regeln und Eigenschaften im Zusammenhang mit adaptiven Headless-Formularen zu erfahren.
