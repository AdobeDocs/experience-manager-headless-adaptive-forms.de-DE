---
title: Aktivieren von adaptiven Headless-Formularen in AEM Forms as a Cloud Service
description: Eine schrittweise Anleitung zur Aktivierung adaptiver Headless-Formulare in AEM Forms as a Cloud Service, die die Einrichtung und Aktivierung in Ihrer Umgebung vereinfacht.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin
level: Beginner, Intermediate
contentOwner: Khushwant Singh
docset: CloudService
hide: true
hidefromtoc: true
exl-id: 7afff771-1296-4162-84c5-c8266b94af2f
source-git-commit: 28792fe1690e68cd301a0de2ce8bff53fae1605f
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 74%

---

# Aktivieren von adaptiven Headless-Formularen in AEM Forms as a Cloud Service {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

Indem Sie adaptive Headless-Formulare in AEM Forms as a Cloud Service aktivieren, können Sie Headless-Formulare mithilfe der AEM Forms Could Service-Instanzen über mehrere Kanäle erstellen, veröffentlichen und versenden. Um adaptive Headless-Formulare verwenden zu können, müssen Sie die Kernkomponenten für adaptive Formulare in Ihrer Umgebung aktivieren.

## Überlegungen

* Bei Erstellung eines neuen AEM Forms as a Cloud Service-Programms [sind adaptive Headless-Formulare für Ihre Umgebungen bereits aktiviert](#are-adaptive-forms-core-components-enabled-for-my-environment).

* Wenn Sie ein älteres Forms as a Cloud Service-Programm ausführen, bei dem Kernkomponenten [nicht aktiviert](#enable-components), fügen Sie zunächst [Abhängigkeiten für adaptive Forms-Kernkomponenten](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment) zu Ihrem Cloud Service-Repository hinzu. Stellen Sie das aktualisierte Repository in jeder Umgebung bereit, um Headless-adaptive Formulare zu aktivieren.

* Wenn Sie in Ihrer Cloud Service-Umgebung bereits [auf Kernkomponenten basierende adaptive Formulare erstellen](create-a-headless-adaptive-form.md) werden Headless-adaptive Formulare automatisch aktiviert. Sie können diese Formulare dann als Headless-Erlebnisse für Mobilgeräte, Web, native Apps oder jeden Service bereitstellen, der sie erfordert.

>[!NOTE]
>
>
> Adobe bietet ein adaptives Forms [Starter Kit (React-App)](create-and-publish-a-headless-form.md) um Entwicklerinnen und Entwicklern zu helfen, schnell mit der Headless Adaptive Forms-Entwicklung zu beginnen, ohne Headless Adaptive Forms in der AEM Forms as a Cloud Service-Umgebung zu aktivieren. Sie können adaptive Headless-Formulare später, nach einer kurzen praktischen Übung zur Erstellung von Headless-Formularen[, in Ihrer Cloud Service-Umgebung aktivieren](create-and-publish-a-headless-form.md).

## Aktivieren von adaptiven Headless-Formularen in einer AEM Forms as a Cloud Service-Umgebung

Führen Sie folgende Schritte in der vorgegebenen Reihenfolge aus, um adaptive Headless-Formulare für eine AEM Forms as a Cloud Service-Umgebung zu aktivieren

<!-- Missing image ALT tag -->
![](/help/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## &#x200B;1. Klonen Sie Ihr AEM Forms as a Cloud Service Git-Repository {#clone-git-repository}

1. Melden Sie sich bei [Cloud Manager](https://my.cloudmanager.adobe.com/) an und wählen Sie Ihre Organisation und Ihr Programm aus.

1. Gehen Sie von Ihrer Seite **Programmübersicht** aus zur Karte **Pipelines**.

1. Klicken Sie auf die **Auf Repository-Informationen zugreifen**, um auf Ihr Git-Repository zuzugreifen und es zu verwalten. Die Seite enthält die folgenden Informationen:

   * Die URL zum Git-Repository von Cloud Manager.
   * Anmeldeinformationen des Git-Repositorys (Benutzername und Password), Git-Benutzername.

   Klicken Sie auf **Kennwort generieren**, um das Kennwort anzuzeigen oder zu generieren.

1. Öffnen Sie das Terminal oder eine Eingabeaufforderung auf Ihrem lokalen Computer und führen Sie den folgenden Befehl aus:

   ```Shell
   git clone [Git Repository URL]
   ```

   Geben Sie bei Aufforderung die Anmeldeinformationen ein. Das Repository wird auf Ihrem lokalen Computer geklont.


## &#x200B;2. Hinzufügen von Abhängigkeiten von Kernkomponenten für adaptive Formulare zu Ihrem Git-Repository {#add-adaptive-forms-core-components-dependencies}

1. Öffnen Sie Ihren Git-Repository-Ordner in einem einfachen Texteditor. Beispiel: VS Code.
1. Öffnen Sie die Datei `[AEM Repository Folder]\pom.xml`, um sie zu bearbeiten.
1. Ersetzen Sie die Versionen der Komponenten `core.forms.components.version`, `core.forms.components.af.version` und `core.wcm.components.version` durch die in der [Dokumentation zu Kernkomponenten](https://github.com/adobe/aem-core-forms-components) angegebenen Versionen. Wenn die Komponente nicht vorhanden ist, fügen Sie diese Komponenten hinzu.

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.forms.components.version>2.0.14</core.formscomponents.version>
       <core.forms.components.af.version>2.0.14</core.forms.components.af.version>  
       <core.wcm.components.version>2.21.2</core.wcmcomponents.version>
   </properties>
   ```

   ![Erwähnung der neuesten Version der Kernkomponenten für adaptive Formulare](/help/assets/latest-forms-component-version.png)

1. Fügen Sie im Abschnitt „Abhängigkeiten“ der Datei `[AEM Repository Folder]\pom.xml` die folgenden Abhängigkeiten hinzu und speichern Sie die Datei.

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
           <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
   <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. Öffnen Sie die Datei `[AEM Repository Folder]/all/pom.xml`, um sie zu bearbeiten. Fügen Sie die folgenden Abhängigkeiten in den Abschnitt `<embeddeds>` ein und speichern Sie die Datei.

   ```XML
   <!-- WCM Core Component Examples Dependencies -->
   
   <!-- inside plugin config of filevault-package-maven-plugin -->  
   <!-- embed wcm core components examples artifacts -->
   
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.config</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <!-- embed forms core components artifacts -->
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   ```

   >[!NOTE]
   >
   >
   >  Ersetzen Sie `${appId}` durch Ihre appId.
   >
   >  Um Ihre `${appId}` zu finden, suchen Sie in der Datei `[AEM Repository Folder]/all/pom.xml` den Begriff `-packages/application/install`. Der Text vor dem Begriff `-packages/application/install` ist Ihre `${appId}`. Der folgende Code `myheadlessform` ist zum Beispiel `${appId}`.
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. Fügen Sie im Abschnitt `<dependencies>` der Datei `[AEM Repository Folder]/all/pom.xml` die folgenden Abhängigkeiten hinzu und speichern Sie die Datei:

   ```XML
           <!-- Other existing dependencies -->
           <!-- wcm core components examples dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <type>zip</type>
               </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
           </dependency>
               <!-- forms core components dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
           </dependency>
               <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
           </dependency>
   ```

1. Öffnen Sie `[AEM Repository Folder]/ui.apps/pom.xml` zur Bearbeitung. Fügen Sie die Abhängigkeit `af-core bundle` hinzu und speichern Sie die Datei.

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >Achten Sie darauf, dass die folgenden Artefakte der Kernkomponenten von adaptiven Formularen nicht in Ihr Projekt eingeschlossen werden.
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-apps</artifactId>`
   >
   > `</dependency>`
   >
   > und
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-core</artifactId>`
   >
   > `</dependency>`


1. Speichern und schließen Sie die Datei.

## &#x200B;3. Aktualisieren Sie das Projekt, um die neueste Version der Forms-Kernkomponenten einzuschließen:

1. Öffnen Sie [AEM-Archetyp-Projektordner]/pom.xml zur Bearbeitung.


1. Speichern und schließen Sie die Datei.

## &#x200B;4. Übertragen Sie die Aktualisierungen in Ihr Git-Repository und führen Sie eine Pipeline aus, um das Repository bereitzustellen {#Commit-the-updates-to-your-git-repository}

1. So übertragen Sie Code in Ihr Git-Repository:
   1. Öffnen Sie das Terminal oder die Eingabeaufforderung.
   1. Navigieren Sie zu Ihrem `[AEM Repository Folder]` und führen Sie die folgenden Befehle in der angegebenen Reihenfolge aus

      ```Shell
      git add pom.xml
      git add all/pom.xml
      git add ui.apps/pom.xml
      git commit -m "Added dependencies for Adaptive Forms Core Components"
      git push origin
      ```

1. Nachdem die Dateien in das Git-Repository übertragen wurden, [führen Sie die Pipeline aus](https://experienceleague.adobe.com/de/docs/experience-manager-cloud-manager/content/using/code-deployment).

   Nach erfolgreicher Pipeline-Ausführung sind die Kernkomponenten von Adaptive Forms für die entsprechende Umgebung aktiviert. Außerdem werden Ihrer Forms as a Cloud Service-Umgebung eine Vorlage für adaptive Formulare (Kernkomponenten) sowie ein Design für Canvas 3.0 hinzugefügt, was Ihnen Optionen zum Anpassen und Erstellen von Kernkomponenten auf Basis von adaptiven Formularen bietet.


## Häufig gestellte Fragen {#faq}

### Was sind die Kernkomponenten? {#core-components}

Die [Kernkomponenten](https://experienceleague.adobe.com/de/docs/experience-manager-core-components/using/introduction) sind eine Reihe standardisierter Web Content Management (WCM)-Komponenten für AEM, die die Entwicklungszeit verkürzen und die Wartungskosten Ihrer Websites senken.

### Welche Funktionen werden hinzugefügt, wenn Kernkomponenten aktiviert sind? {#core-components-capabilities}

Wenn die Kernkomponenten für adaptive Formulare für Ihre Umgebung aktiviert sind, werden Ihrer Umgebung eine leere, auf Kernkomponenten basierende Vorlage für adaptive Formulare und ein Canvas 3.0-Design hinzugefügt. Nachdem Sie die Kernkomponenten der adaptiven Formulare für Ihre Umgebung aktiviert haben, können Sie Folgendes tun:

* Erstellen Sie adaptive Formulare auf Grundlage der Kernkomponenten.
* Erstellen Sie Vorlagen für adaptive Formulare auf Grundlage der Kernkomponenten.
* Erstellen Sie benutzerdefinierte Vorlagen-Designs für adaptive Formulare auf Grundlage der Kernkomponenten.
* Stellen Sie JSON-Darstellungen adaptiver Formulare auf Grundlage der Kernkomponenten für Kanäle wie Mobile, Web, native Apps und Dienste bereit, die eine Headless-Darstellung des Formulars erfordern.

### Sind für meine Umgebung Kernkomponenten für adaptive Formulare aktiviert? {#enable-components}

So prüfen Sie, ob die Kernkomponenten für adaptive Formulare für Ihre Umgebung aktiviert sind:

1. [Klonen Sie Ihr AEM Forms as a Cloud Service-Repository](#1-clone-your-aem-forms-as-a-cloud-service-git-repository).

1. Öffnen Sie die Datei `[AEM Repository Folder]/all/pom.xml` Ihres AEM Forms as a Cloud Service-Git-Repositorys.

1. Suchen Sie nach den folgenden Abhängigkeiten:

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content


   ![Suchen Sie das Artefakt „core-forms-components-af-core“ in „all/pom.xml“.](/help/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   Wenn die Abhängigkeiten vorhanden sind, sind die Kernkomponenten für adaptive Formulare für Ihre Umgebung aktiviert.
