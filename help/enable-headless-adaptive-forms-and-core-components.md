---
title: Aktivieren von adaptiven Headless-Formularen in AEM 6.5 Forms
seo-title: Step-by-Step Guide for enabling Headless Adaptive Forms on AEM 6.5 Forms
description: In unserer Schritt-für-Schritt-Anleitung erfahren Sie, wie Sie in AEM 6.5 Forms adaptive Headless-Formulare aktivieren können. Unser Tutorial führt Sie durch den Prozess, wodurch Sie diese leistungsstarke Funktion einfach in Ihre Website integrieren und Ihr Kundenerlebnis verbessern können.
seo-description: Learn how to enable headless adaptive forms on AEM 6.5 Forms with our step-by-step guide. Our tutorial walks you through the process, making it easy to integrate this powerful feature into your website and improve your user experience.
contentOwner: Khushwant Singh
role: Admin
exl-id: e1a5e7e0-d445-4cca-b8d7-693d9531f075
source-git-commit: 999c3d092d03d7a82363bc94ce79ceb33bf0df7e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Aktivieren von adaptiven Headless-Formularen in AEM 6.5 Forms {#enable-headless-adaptive-forms-on-aem-65-forms}

Um adaptive Headless-Formulare in Ihrer AEM 6.5 Forms-Umgebung zu aktivieren, richten Sie ein auf AEM Archetyp 41 oder höher-basierendes Projekt ein und stellen Sie es für alle Ihre Authoring- und Publishing-Instanzen bereit.

Durch die Bereitstellung des auf AEM Archetyp 41 oder höher-basierenden Projekts auf Ihren AEM 6.5 Forms-Instanzen erhalten Sie die Möglichkeit, [auf Kernkomponenten basierende adaptive Formulare zu erstellen](create-a-headless-adaptive-form.md). Diese Formulare werden im JSON-Format dargestellt und als adaptive Headful- und Headless-Formulare verwendet, was eine größere Flexibilität und Anpassung über verschiedene Kanäle ermöglicht, darunter Mobile, Web und native Apps.

## Voraussetzungen {#prerequisites}

Vor der Aktivierung von adaptiven Headless-Formularen in der AEM 6.5 Forms-Umgebung:

* [Nehmen Sie ein Upgrade auf AEM 6.5 Forms Service Pack 16 (6.5.16.0) oder höher vor](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=de).

* Installieren Sie die neueste Version von [Apache Maven](https://maven.apache.org/download.cgi).

* Installieren Sie einen Nur-Text-Editor. Beispielsweise Microsoft Visual Studio Code.

## Erstellen Sie ein auf dem neuesten AEM Archetyp basierendes Projekt und stellen Sie es bereit

So erstellen Sie ein auf AEM Archetyp 41 oder [höher](https://github.com/adobe/aem-project-archetype) basierendes Projekt und stellen es für alle Authoring- und Publishing-Instanzen bereit:

1. Melden Sie sich bei Ihrem Computer an, hosten Sie Ihre AEM 6.5 Forms-Instanz und führen Sie sie als Administrator aus.
1. Öffnen Sie die Eingabeaufforderung oder das Terminal.
1. Führen Sie den folgenden Befehl aus, um ein auf AEM-Archetyp 41 basierendes Projekt zu erstellen:

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
      -D aemVersion="6.5.15" 
   ```

   * Linux oder Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   Beachten Sie beim Ausführen des oben genannten Befehls die folgenden Punkte:

   * Aktualisieren Sie den Befehl, um die spezifischen Werte für Ihre Umgebung widerzuspiegeln, einschließlich appTitle, appId und groupId. Legen Sie außerdem die Werte für includeFormsenrollment auf „y“ fest. Wenn Sie Forms Portal verwenden, legen Sie die Option _includeExamples=y_ fest, um die Kernkomponenten von Forms Portal in Ihr Projekt aufzunehmen.

   * Ändern Sie „aemVersion“ nicht von 6.5.15.0 in etwas Anderes.

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

      ![Erwähnung der neuesten Version der Forms-Kernkomponenten](/help/assets/latest-forms-component-version.png)

   1. Speichern und schließen Sie die Datei.


1. Nachdem das AEM-Archetyp-Projekt erfolgreich erstellt wurde, erstellen Sie das Bereitstellungspaket für Ihre Umgebung. Erstellen des Pakets:

   1. Navigieren Sie zum Stammverzeichnis Ihres AEM-Archetyp-Projekts.


   1. Führen Sie den folgenden Befehl aus, um das AEM-Archetyp-Projekt für Ihre Umgebung zu erstellen:

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](assets/corecomponent-build-successful.png)


   Nachdem das AEM-Archetyp-Projekt erfolgreich erstellt wurde, wird ein AEM-Paket generiert. Sie finden das Paket im [AEM-Archetyp-Projektordner]\all\target\[appid].all-[version].zip

1. Verwenden Sie den [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=de) zur Bereitstellung des Pakets [AEM-Archetyp-Projektordner]\all\target\[appid].all-[version].zip auf allen Authoring- und Publishing-Instanzen.

>[!NOTE]
>
>
>
>Falls Sie Schwierigkeiten beim Zugriff auf das Anmeldedialogfeld auf einer Publishing-Instanz haben, um das Paket über den Package Manager zu installieren, versuchen Sie, sich über die folgende URL anzumelden: http://[Veröffentlichungs-Server-URL]:[PORT]/system/console. Auf diese Weise können Sie auf die Anmeldung bei der Publishing-Instanz zugreifen, sodass Sie mit dem Installationsprozess fortfahren können.


Die Kernkomponenten sind für Ihre Umgebung aktiviert. Eine leere, auf Kernkomponenten basierende Vorlage für ein adaptives Formular und ein Canvas 3.0-Design werden in Ihrer Umgebung bereitgestellt, sodass Sie [auf Kernkomponenten basierende adaptive Formulare erstellen können](create-a-headless-adaptive-form.md).

## Häufig gestellte Fragen

### Was sind Kernkomponenten?

Die [Kernkomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=de) sind eine Reihe standardisierter Web-Content-Management-Komponenten (WCM) für AEM, um die Entwicklungszeit zu verkürzen und die Wartungskosten Ihrer Websites zu senken.

### Welche Funktionen werden durch die Aktivierung der Kernkomponenten hinzugefügt?


Wenn die Kernkomponenten für adaptive Formulare für Ihre Umgebung aktiviert sind, werden Ihrer Umgebung eine leere, auf Kernkomponenten basierende Vorlage für adaptive Formulare und ein Canvas 3.0-Design hinzugefügt. Nachdem Sie die Kernkomponenten der adaptiven Formulare für Ihre Umgebung aktiviert haben, können Sie Folgendes tun:

* Erstellen Sie adaptive Formulare auf Grundlage der Kernkomponenten.
* Erstellen Sie Vorlagen für adaptive Formulare auf Grundlage der Kernkomponenten.
* Erstellen Sie benutzerdefinierte Vorlagen-Designs für adaptive Formulare auf Grundlage der Kernkomponenten.
* Stellen Sie JSON-Darstellungen adaptiver Formulare auf Grundlage der Kernkomponenten für Kanäle wie Mobile, Web und native Apps und Dienste bereit, die eine Headless-Darstellung des Formulars erfordern.
