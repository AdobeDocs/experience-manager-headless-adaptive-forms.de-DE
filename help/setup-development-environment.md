---
title: Einrichten einer Entwicklungsumgebung für adaptive AEM Headless-Formulare
description: Einrichten einer Entwicklungsumgebung für adaptive AEM Headless-Formulare
hide: true
exl-id: fd92f057-1217-42f8-a454-1bc7e3827e01
source-git-commit: 28792fe1690e68cd301a0de2ce8bff53fae1605f
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 69%

---


# Einrichten einer lokalen Entwicklungsumgebung {#headless-adaptive-forms-setup-development-environment}

Sie können eine lokale Entwicklungsumgebung einrichten, um adaptive Headless-Formulare auf Ihrem lokalen Computer zu erstellen und zu testen. Die Entwicklungsumgebung besteht aus dem AEM SDK- und AEM Forms-Funktionsarchiv, die auf AEM SDK installiert sind.
<!--
 After a Headless adaptive form or related assets are ready on the local development environment, you can deploy the Headless adaptive form application to your publishing environment. -- >

You require knowledge to build application using react, Git, and Maven to use Headless adaptive forms.

<!-- 

### Download the latest version of AEM as a Cloud Service SDK or Forms feature archive (AEM Forms add-on) from Software Distribution {#software-distribution}

To download the supported version of Adobe Experience Manager as a Cloud Service SDK or Forms feature archive (AEM Forms add-on):

1. Log in to [Software Distribution](https://experience.adobe.com/#/downloads) portal with your Adobe ID.

    >[!NOTE]
    >
    > Your Adobe Organization must be provisioned for AEM as a Cloud Service to download the AEM as a Cloud Service SDK.

1. Navigate to the **[!UICONTROL AEM as a Cloud Service]** tab.
1. Sort by published date in descending order.
1. Click on the latest Adobe Experience Manager as a Cloud Service SDK or Forms feature archive (AEM Forms add-on).
1. Review and accept the EULA. Tap the **[!UICONTROL Download]** button. -->

## Systemanforderungen {#headless-adaptive-forms-system-requirements}

Um AEM SDK zu installieren, muss Ihr lokaler Computer die folgenden Mindestanforderungen erfüllen:

* [Java Development Kit 11](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&fulltext=Oracle%7E+JDK%7E+11%7E&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=14)
* [Die neueste Version von Git](https://git-scm.com/downloads). Wenn Sie mit Git noch nicht vertraut sind, lesen Sie [Installieren von Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
* [Node.js 16.13.0 oder höher](https://nodejs.org/de/download/). <!-- URL is 404! If you are new to Node.js, see [How to install Node.js](https://nodejs.dev/en/learn/how-to-install-nodejs). -->
* [Maven 3.6 oder höher](https://maven.apache.org/download.cgi). Wenn Sie mit Maven noch nicht vertraut sind, lesen Sie [Installieren von Apache Maven](https://maven.apache.org/install.html).

## Einrichten einer Entwicklungsumgebung {#headless-adaptive-forms-procedure-to-setup-development-environment}

So richten Sie eine neue lokale Entwicklungsumgebung ein und verwenden sie zum Entwickeln und Testen von adaptiven Headless-Formularen:

1. [Richten Sie das AEM as a Cloud Service SDK ein](#setup-author-instance).
1. [AEM Forms-Archiv (AEM Forms Cloud Service-Add-on) zur AEM SDK hinzufügen](#add-forms-archive).

<!--

1. (Optional) [Add Forms-specific users to your local Author instance](#configure-users-and-permissions).
1. (Optional) Install [Adaptive forms builder extension for Microsoft Visual Studio Code](#microsoft-visual-studio-code-extension-for-headless-adaptive-forms). 

-->

### &#x200B;1. Richten Sie das AEM as a Cloud Service SDK ein {#setup-author-instance}

AEM as a Cloud Service SDK (AEM SDK) bietet Entwicklerinnen und Entwicklern eine lokale Erfahrung zum Erstellen und Testen von adaptiven Headless-Formularen. Sie können das AEM as a Cloud Service SDK verwenden, um adaptive Headless-Formulare zu erstellen und in der Vorschau anzuzeigen, sodass Sie die meisten Überprüfungen im Zusammenhang mit der Entwicklung lokal durchführen können. So richten Sie eine lokale Autoreninstanz ein:

1. [Laden Sie die](https://experience.adobe.com/#/downloads/content/software-distribution/de/aemcloud.html) neueste [!DNL Adobe Experience Manager] as a Cloud Service SDK herunter. Verwenden Sie die Spalte „Veröffentlichungsdatum“, um die Liste zu sortieren und das neueste SDK einfach zu finden.
Es liegt im ZIP-Format vor. Die unterstützte Version ist aem-sdk-2022.7.8085.20220725T140323Z-220700.zip und höher.

   ![Herunterladen des AEM Cloud Service SDK vom Software Distribution-Portal](assets/software-distribution.png)


1. Extrahieren Sie die heruntergeladene ZIP-Datei in ein Verzeichnis auf Ihrem lokalen Computer.
1. Erstellen Sie auf Ihrem lokalen Computer ein Verzeichnis, das als Installationsspeicherort für die Autoreninstanz dient. Zum Beispiel: `~/aem-sdk/author`.
1. Kopieren Sie die JAR-Datei aus den extrahierten SDK-Dateien in den Installationsspeicherort und benennen Sie die Datei in `aem-author-p4502.jar` um. Die Zeichenfolge `p4502` im Dateinamen gibt die zu verwendende Port-Nummer an. Sie können auch eine andere Port-Nummer angeben.

   >[!NOTE]
   >
   > Doppelklicken Sie nicht auf die JAR-Datei, um sie zu starten. Dies führt zu einem [Fehler](https://experienceleague.adobe.com/de/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime#troubleshooting-double-click).

1. Öffnen Sie eine Eingabeaufforderung:
   * Verwenden Sie unter Windows die Option **Als Administrator ausführen**, um die Eingabeaufforderung im erhöhten Modus zu öffnen.
   * Stellen Sie unter Linux® sicher, dass Sie das Terminal-Fenster als Root-Benutzer öffnen.

1. Navigieren Sie zum Installationsspeicherort mit der kopierten JAR-Datei und führen Sie den folgenden Befehl aus:

   `java -jar aem-author-p4502.jar -r prerelease`

   ![Herunterladen des AEM Cloud Service SDK vom Software Distribution-Portal](assets/install-sdk.png)

   * Mit dem `-r prerelease` Switch werden die Funktionen aktiviert, die nur im Rahmen der Vorabversionsprogramme und der eingeschränkten Veröffentlichungsprogramme verfügbar sind.
   * Sie können `admin` als Benutzername und Kennwort für die lokale Entwicklung verwenden, um sich nicht so viel merken zu müssen.

   Nach dem Start von AEM wird die Anmeldeseite im Webbrowser geöffnet. Sie können auch die Anmeldeseite für AEM SDK-Instanz unter der Adresse `http://localhost:<port>` in Ihrem Webbrowser öffnen. Beispiel: [http://localhost:4502](http://localhost:4502).

1. Melden Sie sich bei Ihrer Autoreninstanz an. Tippen Sie auf das ![Hilfe](/help/assets/Help-icon.svg)-Symbol und dann auf „Info zu Adobe Experience Manager“ und stellen Sie sicher, dass die Versionsnummer das PRERELEASE-Postfix enthält.

   ![Hilfe](/help/assets/prerelease.png)

Wenn das PRERELEASE-Postfix nicht angezeigt wird, stoppen Sie den Server, löschen Sie den `[AEM SDK installation]/crx-quickstart folder` und starten Sie die .jar-Datei des AEM SDK mit dem Schalter `-r prerelease` neu. Weitere Optionen finden Sie unter [Fehlerbehebung](/help/troubleshooting.md).

### &#x200B;2. Fügen Sie das AEM Forms-Archiv (AEM Forms Cloud Service-Add-On) zum AEM SDK hinzu {#add-forms-archive}

Das AEM Forms as a Cloud Service-Funktionsarchiv (AEM Forms Cloud Service-Add-on) bietet Tools zum Erstellen von Headless-adaptiven Formularen in einer lokalen Entwicklungsumgebung. So installieren Sie das Funktionsarchiv:

1. Laden Sie die neueste Version des [!DNL AEM Forms]-Funktionsarchivs (AEM Forms-Add-on) über [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/de/aemcloud.html?fulltext=AEM*+Forms*+add*+on*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=20) herunter und extrahieren Sie sie. Verwenden Sie die Spalte „Veröffentlichungsdatum“, um die Liste zu sortieren und das neueste SDK einfach zu finden. Die unterstützte Version ist aem-forms-addon-2022.07.06.02-220600 und höher.

1. Navigieren Sie zum Verzeichnis „crx-quickstart/install“. Wenn der Ordner nicht vorhanden ist, erstellen Sie ihn.
1. Stoppen Sie Ihre AEM SDK-Instanz. Sie können das Eingabeaufforderungsfenster beenden, in dem eine AEM SDK-Instanz ausgeführt wird, um AEM zu stoppen.
1. Kopieren Sie das [!DNL AEM Forms]-Add-On mit dem Funktionsarchiv aus der Datei `aem-forms-addon-<version>.far`, die in Schritt 1 in den Installationsordner extrahiert wurde.
1. Verwenden Sie den folgenden Befehl, um die AEM SDK-Instanz neu zu starten:

   `java -jar aem-author-p4502.jar -r prerelease`

<!-- 

### 3. (Optional) Configure users and permissions {#configure-users-and-permissions}

Create seperate user accounts for Form Developer, Form Practitioner, and end users. These account help you test Headless adaptive forms for various types of users. To create a user account and add roles to the account:

1. Login to your AEM SDK instance.
1. Go to Tools > Security > Users and tap Create. The Create New User wizard opens.
1. In the details tab, specify an ID and Password. All other fields are optional. It is recommended to provide name and an email address.
1. In the Groups tab, search and select user-groups for a user depending on their role. The table below lists all types of users and pre-defined groups for each type of forms users based on their role:
  
    | User Type | AEM Group |
    |---|---|
    | Form developer | [!DNL forms-users] (AEM Forms Users), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors], and [!DNL fdm-authors]  |
    | Customer Experience Lead or UX Designer| [!DNL forms-users], [!DNL template-authors]|
    | AEM administrator | [!DNL aem-administrators], [!DNL fd-administrators] |
    | End user| When a user must log in to view and submit an Adaptive Form, add such users to [!DNL forms-users] group. </br> When no user authentication is required to access Adaptive Forms, do not assign any group to such users.|

<!-- ### 4. (Optional) Install Visual Studio Code extension for Headless adaptive forms {#microsoft-visual-studio-code-extension-for-headless-adaptive-forms}

You can use any IDE for developing Headless adaptive forms. Adobe provides an extension for Microsoft&reg;reg; Visual Studio Code to make it easier for you to navigate structure and develop Headless adaptive forms. The extension adds adaptive forms related IntelliSense capabilities and helps auto-complete Headless adaptive forms JSON syntax. It also adds a panel, titled Forms Tree, to help navigate structure of Headless adaptive form. To use the extension: 

1. Ensure [Microsoft Visual Studio Code 1.62.0 or later](https://code.visualstudio.com/docs/supporting/FAQ#_how-do-i-find-the-version) is installed. If you have an older version or no version installed, download the latest version from [Microsoft Website](https://code.visualstudio.com/docs/setup/setup-overview)
   >[!NOTE]
   >
   >
   > To use Visual Studio from command line on macOS, see [Launching from the command line](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line).

1. Download the [Adaptive forms builder extension](/help/assets/adaptive-form-builder-0.12.0.vsix).

1. Navigate the directory containing the *adaptive-form-builder-[version].vsix* file.

1. Run the following command or see [Install from a VSIX](https://code.visualstudio.com/docs/editor/extension-marketplace#_install-from-a-vsix) article for detailed instructions to install a Visual Studio Code extension from a VSIX file:

    `code -–install-extension adaptive-form-builder-[version].vsix`

    </br> Replace the [version] with actual version of the extension. For example, `code -–install-extension adaptive-form-builder-0.12.0.vsix`

    </br> 

    ![Installing extension](/help/assets/install-extension.png)

<!-- ## Create and setup a react app

Adaptive forms renderer component is a react based component. It requires a react app to run and render a Headless adaptive form. To create and setup react app:

1. Open terminal in Visual Studio code and run the following command to create a react app and installs all related dependencies:

    ```shell
    npx create-react-app [react-app-name] --scripts-version 4.0.3 --template typescript
    ```

    Where [react-app-name] represents name of the project, script version is 4.0.3, and template of type typescript. For example, the following command creates a react app named *headless-forms-demo*.

    ```shell
    npx create-react-app headless-forms-demo --scripts-version 4.0.3 --template typescript
    ```

    It may take some time to create the react app and install all the dependencies. The command creates an empty react app with latest version of react and react-dom dependencies. It does not have any artifacts related to adaptive forms renderer component.

1. Adaptive forms renderer component is based on react spectrum and requires react 16.0.0 and react-dom 16.0.0. To install react 16.0.0 and related dependencies:
    1. Open the Visual Studio code terminal Window or command prompt.
    1. Navigate to the directory of react project.  
    1. Run the following command:

        ```shell
        npm install --save react@16.0.0 react-dom@16.14.0 -force
        ```

1. Run the following command to install adaptive forms renderer component related dependencies:

    ```shell
    npm i --save @aemforms/forms-super-component @aemforms/forms-react-core-components @aemforms/forms-super-component @adobe/react-spectrum @react/react-spectrum
    ```

<!-- 1. Install dependencies for adaptive forms renderer component. Packages for these dependencies are available in Adobe Artifactory. To authenticate with Adobe Artifactory and install dependencies for adaptive forms renderer component:

    1. Create environment variables ARTIFACTORY_USER and ARTIFACTORY_API_TOKEN. The ARTIFACTORY_USER stores Adobe LDAP username and ARTIFACTORY_API_TOKEN stores your [Adobe Artifactory token](https://wiki.corp.adobe.com/display/Artifactory/API+Keys)

    1. Run the following command to set NPM_TOKEN and NPM_EMAIL tokens:

        ```shell

        auth=$(curl -s -u${ARTIFACTORY_USER}:${ARTIFACTORY_API_TOKEN} https://artifactory.corp.adobe.com/artifactory/api/npm/auth)
        export NPM_TOKEN=$(echo "${auth}" | grep "_auth" | awk -F " " '{ print $3 }')
        export NPM_EMAIL=$(echo "${auth}" | grep "email" | awk -F " " '{ print $3 }')
        ```

        These tokens are required to communicated with Adobe Artifactory.

    1. Create a .npmrc file in the react project.

        ![.npmrc file](/help/assets/npmrc.png)

    1. Add the following code to the file:

        ```shell
        @aemforms:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-release/
        @react:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-react-release/
        @quarry:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-adobe-release-local/
        //artifactory.corp.adobe.com/artifactory/api/npm/npm-adobe-release-loca/:_auth=${NPM_TOKEN}
        //artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-release/:_auth=${NPM_TOKEN}
        //artifactory.corp.adobe.com/artifactory/api/npm/npm-react-release/:_auth=${NPM_TOKEN}
        _auth=${NPM_TOKEN}
        email=${NPM_EMAIL}
        always-auth=true
        ```

        It defines the antifactory repositories to use for Headless adaptive forms, react, and quarry related scope.
    1. Run the following command to install adaptive forms renderer component related dependencies:

    ```shell
    npm i --save @aemforms/crispr-react-bindings @aemforms/crispr-react-core-components @adobe/react-spectrum @react/react-spectrum
    ```
 
-->
Ihre lokale Umgebung ist bereit. Sie können mit dem Erstellen eines adaptiven Headless-Formulars fortfahren.
