---
title: Aktivieren von adaptiven Headless-Formularen in AEM 6.5 Forms
seo-title: Step-by-Step Guide for enabling Headless Adaptive Forms on AEM 6.5 Forms
description: Erfahren Sie mit der schrittweisen Anleitung von Adobe, wie Sie Headless Adaptive Forms auf AEM 6.5 Forms aktivieren. Dieses Tutorial führt Sie durch den Prozess, der es Ihnen erleichtert, diese leistungsstarke Funktion in Ihre Website zu integrieren und Ihr Benutzererlebnis zu verbessern.
contentOwner: Khushwant Singh
role: Admin
exl-id: e1a5e7e0-d445-4cca-b8d7-693d9531f075
source-git-commit: 28792fe1690e68cd301a0de2ce8bff53fae1605f
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 70%

---

# Aktivieren von adaptiven Headless-Formularen in AEM 6.5 Forms {#enable-headless-adaptive-forms-on-aem-65-forms}

Um adaptive Headless-Formulare in Ihrer AEM 6.5 Forms-Umgebung zu aktivieren, richten Sie ein auf AEM Archetyp 41 oder höher-basierendes Projekt ein und stellen Sie es für alle Ihre Authoring- und Publishing-Instanzen bereit.

Durch die Bereitstellung des auf AEM Archetyp 41 oder höher-basierenden Projekts auf Ihren AEM 6.5 Forms-Instanzen erhalten Sie die Möglichkeit, [auf Kernkomponenten basierende adaptive Formulare zu erstellen](create-a-headless-adaptive-form.md). Diese Formulare werden im JSON-Format dargestellt und sowohl als `Headful` als auch als `Headless` adaptives Forms verwendet, was eine größere Flexibilität und Anpassung über eine Reihe von Kanälen hinweg ermöglicht, einschließlich mobiler, Web- und nativer Apps.

## Voraussetzungen {#prerequisites}

Bevor Sie Headless Adaptive Forms in der AEM 6.5 Forms-Umgebung aktivieren,

* [Nehmen Sie ein Upgrade auf AEM 6.5 Forms Service Pack 16 (6.5.16.0) oder höher vor](https://experienceleague.adobe.com/de/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions).

* Installieren Sie die neueste Version von [Apache Maven](https://maven.apache.org/download.cgi).

* Installieren Sie einen Nur-Text-Editor. Beispielsweise Microsoft Visual Studio Code.

## Erstellen und Bereitstellen des neuesten AEM Archetype-basierten Projekts

So erstellen Sie ein auf AEM Archetyp 41 oder [höher](https://github.com/adobe/aem-project-archetype) basierendes Projekt und stellen es für alle Authoring- und Publishing-Instanzen bereit:

1. Melden Sie sich bei Ihrem Computer an, hosten Sie Ihre AEM 6.5 Forms-Instanz und führen Sie sie als Administrator aus.
1. Öffnen Sie die Eingabeaufforderung oder das Terminal.
1. Führen Sie den folgenden Befehl aus, um ein auf AEM Archetype 41 basierendes Projekt zu erstellen:

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.23" 
   ```

   * Linux® oder Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.23" 
   ```

   Beachten Sie beim Ausführen des obigen Befehls Folgendes:

   * Aktualisieren Sie den Befehl, um die spezifischen Werte für Ihre Umgebung widerzuspiegeln, einschließlich appTitle, appId und groupId. Legen Sie außerdem die Werte für includeFormsEnrollment auf `y` fest. Wenn Sie Forms Portal verwenden, legen Sie die Option _includeExamples=y_ fest, um die Kernkomponenten von Forms Portal in Ihr Projekt aufzunehmen.


1. (Nur für Projekte, die auf dem Archetyp Version 41 basieren) Nachdem das AEM-Archetyp-Projekt erstellt wurde, aktivieren Sie Designs für auf Kernkomponenten basierende adaptive Formulare. So aktivieren Sie Designs:

   1. Öffnen Sie den [AEM-Archetyp-Projektordner]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html zur Bearbeitung:

   1. Fügen Sie in Zeile 21 den folgenden Code hinzu:

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Fügen Sie den oben genannten Code in Zeile 21 hinzu](/help/assets/code-to-enable-themes.png)

   1. Speichern und schließen Sie die Datei.

1. Aktualisieren Sie das Projekt, um die neueste Version der Forms-Kernkomponenten einzuschließen:

   1. Öffnen Sie den [AEM-Archetyp-Projektordner]/pom.xml zur Bearbeitung.
   1. Legen Sie die Version von `core.forms.components.version` und `core.forms.components.af.version` auf die [neueste Version der Forms-Kernkomponenten](https://github.com/adobe/aem-core-forms-components/tree/release/650) fest.

   1. Speichern und schließen Sie die Datei.


1. Nachdem das AEM-Archetyp-Projekt erfolgreich erstellt wurde, erstellen Sie das Bereitstellungspaket für Ihre Umgebung. Erstellen des Pakets:

   1. Navigieren Sie zum Stammverzeichnis Ihres AEM-Archetyp-Projekts.


   1. Führen Sie den folgenden Befehl aus, um das AEM-Archetyp-Projekt für Ihre Umgebung zu erstellen:

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](assets/corecomponent-build-successful.png)


   Nachdem das AEM-Archetyp-Projekt erfolgreich erstellt wurde, wird ein AEM-Paket generiert. Sie finden das Paket im [AEM-Archetyp-Projektordner]\all\target\[appid].all-[version].zip

1. Verwenden Sie den [Package Manager](https://experienceleague.adobe.com/de/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager) zur Bereitstellung des Pakets [AEM-Archetyp-Projektordner]\all\target\[appid].all-[version].zip auf allen Authoring- und Publishing-Instanzen.

>[!NOTE]
>
>
>
>Wenn Sie auf Schwierigkeiten stoßen, das Anmelde-Dialogfeld auf einer Veröffentlichungsinstanz aufzurufen, um das Paket über den Package Manager zu installieren, versuchen Sie, sich über die folgende URL anzumelden: `http://[Publish Server URL]`:[PORT]/system/console. Über diesen Prozess erhalten Sie Zugriff auf die Anmeldung bei der Veröffentlichungsinstanz und können den Installationsprozess fortsetzen.


Die Kernkomponenten sind für Ihre Umgebung aktiviert. Eine leere, auf Kernkomponenten basierende Vorlage für ein adaptives Formular und ein Canvas 3.0-Design werden in Ihrer Umgebung bereitgestellt, sodass Sie [auf Kernkomponenten basierende adaptive Formulare erstellen können](create-a-headless-adaptive-form.md).

## Häufig gestellte Fragen

### Was sind die Kernkomponenten?

Die [Kernkomponenten](https://experienceleague.adobe.com/de/docs/experience-manager-core-components/using/introduction) sind eine Reihe standardisierter Web Content Management (WCM)-Komponenten für AEM, die die Entwicklungszeit verkürzen und die Wartungskosten Ihrer Websites senken.

### Welche Funktionen werden durch die Aktivierung der Kernkomponenten hinzugefügt?


Wenn die Kernkomponenten für adaptive Formulare für Ihre Umgebung aktiviert sind, werden Ihrer Umgebung eine leere, auf Kernkomponenten basierende Vorlage für adaptive Formulare und ein Canvas 3.0-Design hinzugefügt. Nachdem Sie die Kernkomponenten der adaptiven Formulare für Ihre Umgebung aktiviert haben, können Sie Folgendes tun:

* Erstellen Sie adaptive Formulare auf Grundlage der Kernkomponenten.
* Erstellen Sie Vorlagen für adaptive Formulare auf Grundlage der Kernkomponenten.
* Erstellen Sie benutzerdefinierte Vorlagen-Designs für adaptive Formulare auf Grundlage der Kernkomponenten.
* Stellen Sie JSON-Darstellungen adaptiver Formulare auf Grundlage der Kernkomponenten für Kanäle wie Mobile, Web und native Apps und Dienste bereit, die eine Headless-Darstellung des Formulars erfordern.
