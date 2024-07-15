---
title: Aktivieren von adaptiven Headless-Formularen in AEM Forms as a Cloud Service
seo-title: Step-by-Step Guide for enabling Headless Adaptive Forms on AEM Forms as a Cloud Service
description: In unserer Schritt-für-Schritt-Anleitung erfahren Sie, wie Sie in AEM Forms as a Cloud Service adaptive Headless-Formulare aktivieren können Unser Tutorial führt Sie durch den Prozess und erleichtert Ihnen so den Einstieg in diese leistungsstarke Funktion Ihrer AEM Forms-Umgebung.
seo-description: Learn how to enable headless adaptive forms on AEM Forms as a Cloud Service with our step-by-step guide. Our tutorial walks you through the process, making it easy to enable this powerful feature for your AEM Forms environment.
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
source-git-commit: 999c3d092d03d7a82363bc94ce79ceb33bf0df7e
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 100%

---

# Aktivieren von adaptiven Headless-Formularen in AEM Forms as a Cloud Service {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

Indem Sie adaptive Headless-Formulare in AEM Forms as a Cloud Service aktivieren, können Sie Headless-Formulare mithilfe der AEM Forms Could Service-Instanzen über mehrere Kanäle erstellen, veröffentlichen und versenden. Um adaptive Headless-Formulare verwenden zu können, müssen Sie die Kernkomponenten für adaptive Formulare in Ihrer Umgebung aktivieren.

## Überlegungen

* Bei Erstellung eines neuen AEM Forms as a Cloud Service-Programms [sind adaptive Headless-Formulare für Ihre Umgebungen bereits aktiviert](#are-adaptive-forms-core-components-enabled-for-my-environment).

* Wenn Sie über ein älteres Forms as a Cloud Service-Programm verfügen, in dem die Kernkomponenten [nicht aktiviert sind](#enable-components), können Sie zu Ihrem AEM as a Cloud Service-Repository [Abhängigkeiten von Kernkomponenten für adaptive Formulare hinzufügen](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment) und dieses in Ihren Cloud Service-Umgebungen nutzen, um adaptive Headless-Formulare zu aktivieren.

* Wenn Ihre bestehende Cloud Service-Umgebung eine Option bietet, [ adaptive Formulare auf Grundlage der Kernkomponenten zu erstellen](create-a-headless-adaptive-form.md), sind adaptive Headless-Formulare in Ihrer Umgebung bereits aktiviert und Sie können sie als Headless-Formulare für Kanäle wie Mobile, Web, native Apps und Dienste bereitstellen, die eine Headless-Darstellung adaptiver Formulare erfordern.


>[!NOTE]
>
>
> Mit dem [Starter-Kit (React-App)](create-and-publish-a-headless-form.md) für adaptive Formulare von Adobe können Entwicklungspersonen schnell und bequem mit adaptiven Headless-Formularen arbeiten, ohne diese Funktion in ihrer AEM Forms as a Cloud Service-Umgebung aktivieren zu müssen. Sie können adaptive Headless-Formulare später, nach einer kurzen praktischen Übung zur Erstellung von Headless-Formularen[, in Ihrer Cloud Service-Umgebung aktivieren](create-and-publish-a-headless-form.md).

## Aktivieren von adaptiven Headless-Formularen in einer AEM Forms as a Cloud Service-Umgebung

Führen Sie folgende Schritte in der vorgegebenen Reihenfolge aus, um adaptive Headless-Formulare für eine AEM Forms as a Cloud Service-Umgebung zu aktivieren


![](/help/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1. Klonen Sie Ihr AEM Forms as a Cloud Service Git-Repository {#clone-git-repository}

1. Melden Sie sich bei [Cloud Manager](https://my.cloudmanager.adobe.com/) an und wählen Sie Ihre Organisation und Ihr Programm aus.

1. Navigieren Sie von Ihrer **Programmübersichtsseite** zur Karte **Pipelines** und klicken Sie auf die Schaltfläche **Zugriff auf Repo Info**, um auf Ihr Git-Repository zuzugreifen und es zu verwalten. Die Seite enthält die folgenden Informationen:

   * Die URL zum Git-Repository von Cloud Manager.
   * Anmeldeinformationen des Git-Repositorys (Benutzername und Password), Git-Benutzername.

   Klicken Sie auf **Kennwort generieren**, um das Kennwort anzuzeigen oder zu generieren.

1. Öffnen Sie das Terminal oder eine Eingabeaufforderung auf Ihrem lokalen Computer und führen Sie den folgenden Befehl aus:

   ```Shell
   git clone [Git Repository URL]
   ```

   Geben Sie bei Aufforderung die Anmeldeinformationen ein. Das Repository wird auf Ihrem lokalen Computer geklont.


## 2. Hinzufügen von Abhängigkeiten von Kernkomponenten für adaptive Formulare zu Ihrem Git-Repository {#add-adaptive-forms-core-components-dependencies}

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

## 3. Aktualisieren Sie das Projekt, um die neueste Version der Forms-Kernkomponenten einzuschließen:

1. Öffnen Sie [AEM-Archetyp-Projektordner]/pom.xml zur Bearbeitung.


1. Speichern und schließen Sie die Datei.

## 4. Übertragen Sie die Aktualisierungen in Ihr Git-Repository und führen Sie die Pipeline aus, um das Repository bereitzustellen {#Commit-the-updates-to-your-git-repository}

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

1. Nachdem die Dateien in das Git-Repository übertragen wurden, [führen Sie die Pipeline aus](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=de).

   Nach erfolgreicher Ausführung der Pipeline sind die Kernkomponenten für adaptive Formulare für die entsprechende Umgebung aktiviert. Außerdem werden Ihrer Forms as a Cloud Service-Umgebung eine Vorlage für adaptive Formulare (Kernkomponenten) sowie ein Design für Canvas 3.0 hinzugefügt, was Ihnen Optionen zum Anpassen und Erstellen von Kernkomponenten auf Basis von adaptiven Formularen bietet.


## Häufig gestellte Fragen {#faq}

### Was sind Kernkomponenten? {#core-components}

Die [Kernkomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=de) sind eine Reihe von standardisierten Web Content Management(WCM)-Komponenten für AEM, die die Entwicklungszeit beschleunigen und die Wartungskosten Ihrer Websites reduzieren.

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
