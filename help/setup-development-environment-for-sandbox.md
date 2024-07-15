---
title: Einrichten einer Entwicklungsumgebung für eine Forms as a Cloud Service-Sandbox
description: Einrichten einer Entwicklungsumgebung für eine Forms as a Cloud Service-Sandbox
hide: true
exl-id: befac9ad-d2c4-4705-96fc-f0ea0ef823b8
source-git-commit: 41286ff4303e0f4d404deb113fd59d1499768da5
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 100%

---

# Einrichten einer Entwicklungsumgebung für adaptive Headless-Formulare in Cloud Service

<span class="preview"> Dieser Artikel wird **FORTLAUFEND ÜBERARBEITET**.</span>


Bereit zum Erstellen und Testen von adaptiven Headless-Formularen in Cloud Service? Aktivieren Sie Formulare für Ihr Cloud Service-Programm und legen Sie los.

## Vorbereitung

* Installieren Sie die [neueste Version von Git](https://git-scm.com/downloads) auf Ihrem lokalen Computer. Wenn Sie mit Git noch nicht vertraut sind, lesen Sie [Installieren von Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git). Sie verwenden das Git-Repository, um die in Ihrer lokalen Entwicklungsumgebung entwickelten Formulare und benutzerdefinierten Code in Ihre Cloud Service-Entwicklungsumgebung zu übertragen.

* Installieren Sie [Node.js 16.13.0 oder höher](https://nodejs.org/de/download/) auf Ihrem lokalen Computer. Wenn Sie mit Node.js noch nicht vertraut sind, lesen Sie die [Installationsanleitung für Node.js](https://nodejs.dev/en/learn/how-to-install-nodejs).

* Erstellen Sie ein AEM as a Cloud Service-Programm: Folgen Sie den Schritten 1 bis 7 des Artikels zum [Erstellen von Programmen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program), um ein Programm für Ihre Organisation zu erstellen.

* Aktivieren Sie den [Vorabversionskanal für Ihr Cloud Service-Programm](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=de&amp;cloud-environments).

## Einrichten des Arbeitsablaufs

Aktivieren Sie zum Aktivieren von adaptiven Headless-Formularen in Ihrer Forms as a Cloud Service-Sandbox die Lösung `Forms - Digital enrolment` für Ihr AEM Cloud Service-Programm, erstellen Sie auf Ihrem lokalen Computer ein auf Archetyp 37 oder höher basierendes Projekt und übertragen Sie es in Ihre Forms as a Cloud Service-Umgebung. Der gesamte Prozess läuft wie folgt ab:

![Workflow zum Einrichten einer Entwicklungsumgebung für eine Forms as a Cloud Service-Sandbox](assets/FORMS-HLAF-SANDBOX-PRODUCTION-ENR.png)

### 1. Aktivieren Sie Forms für Ihr Programm

<table style="table-layout:auto">
<tr>
  <td>
  1. Melden Sie sich bei <a href="https://experience.adobe.com/" >https://experience.adobe.com/</a> an und wählen Sie die Option <b>Experience Manager</b>.
  </td>
  <td>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program">
      <img alt="AEM as a Cloud Service-Programme" src="assets/cloud-manager-experience-manager.png">
    </a>
    <br>
  </td>
</tr>
<tr>
  <td>
  2. Klicken Sie für die Option <b>Cloud Manager</b> auf <b>Starten. </b> Eine Liste der Programme für Ihre Organisation wird angezeigt.
  </td>
  <td>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program">
      <img alt="AEM as a Cloud Service-Programme" src="assets/cloud-manager-experience-manager-launch.png">
    </a>
    <br>
  </td>
</tr>
<tr>
  <td>
    3. Tippen Sie für Ihr Programm auf das Symbol „…“ und wählen Sie die Option <b>Programm bearbeiten</b>. Ein Dialogfeld wird angezeigt. 
  </td>
  <td>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program">
      <img alt="AEM as a Cloud Service-Programme" src="assets/edit-program.png">
    </a>
    <br>
  </td>
</tr>
<tr>
  <td>
    4. Navigieren Sie im Dialogfeld „Programm bearbeiten“ zur <b>Registerkarte „Lösungen und Add-ons“</b>, wählen Sie die Option <b>Forms – Digitale Registrierung</b> und tippen Sie auf <b>Aktualisieren</b>. 
  </td>
  <td>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program">
      <img alt="AEM as a Cloud Service-Programme" src="assets/program-solution-addons.png">
    </a>
    <br>
  </td>
</tr>
</table>

### 2. Klonen Sie das Git-Repository Ihres Programms auf Ihrem lokalen Computer

Jedes AEM as a Cloud Service-Programm verfügt über ein Git-Repository. Sie können damit benutzerdefinierten Code und Assets von einem lokalen Computer in Ihre Cloud Service-Umgebung hochladen. Während des Setups verwenden wir das Git-Repository, um auf adaptive Headless-Formulare bezogenen Code, Vorlagen und andere Informationen von Ihrem Cloud Service-Programm auf Ihren lokalen Computer zu übertragen. Das Klonen des Cloud Service-Git-Repositorys auf Ihrem lokalen Computer ist der erste Schritt, um benutzerdefinierten Code und Inhalte von Ihrem lokalen Computer in den Cloud Service zu übertragen.

>[!INFO]
>
> Sie können jederzeit ein Git-Repository nutzen, ohne es zu klonen. Dies hat jedoch seine eigenen Tücken. Wir verwenden in diesem Dokument also den Klonansatz.


So klonen Sie das Repository:

<table style="table-layout:fixed">
<tr>
  <td>
  1. Tippen Sie im Pipeline-Feld Ihres Programms auf <b>Zugriff auf Repo Info. </b> Ein Dialogfeld mit Repository-Informationen wird angezeigt 
  </td>
  <td>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program">
      <img alt="AEM as a Cloud Service-Programme" src="assets/git-repo.png">
    </a>
    <br>
  </td>
</tr>
<tr>
  <td>
  2. Tippen Sie auf <b>Kennwort generieren</b> und kopieren Sie die <b>Repository-URL. </b> 
  </td>
  <td>
      <img alt="AEM as a Cloud Service-Programme" src="assets/repository-info.png">
    <br>
  </td>
</tr>
<tr>
  <td>
    3. Öffnen Sie auf Ihrem lokalen Computer die Eingabeaufforderung, erstellen Sie einen Ordner, führen Sie den folgenden Befehl aus und geben Sie nach Aufforderung die Repository-Anmeldeinformationen ein:
 </br>
 <code> git clone [Repository URL] </code> </br></br>
 Beispiel: </br> 
    <code> git clone https://git.cloudmanager.adobe.com/stage-aemformsdev/khushwantsingh-p45413-uk89613/ </code>

</br> Wenn Sie aufgefordert werden, rufen Sie den <b>Benutzernamen</b> und das <b>Passwort</b> aus dem Fenster <b>Repository-Informationen</b> ab.
</td>
  <td>
     <img alt="AEM as a Cloud Service-Programme" src="assets/clone-success.png">
  </td>
</tr>
</table>


### 3. Erstellen Sie ein AEM Archetyp-basiertes Projekt

Das Archetyp-Projekt ist eine Maven-basierte Vorlage. Es wird ein minimales Projekt basierend auf Best Practices erstellt, um mit adaptiven Headless-Formularen zu beginnen. Es enthält auch die Kernfunktionen für adaptive Headless-Formulare für Forms as a Cloud Service. Es ist erforderlich, das auf Archetyp 37 oder höher basierende Projekt zu erstellen und bereitzustellen.
®®®
Führen Sie je nach Betriebssystem den Maven-Befehl aus, um ein Experience Manager Forms as a Cloud Service-Projekt zu erstellen. Verwenden Sie den Archetyp Version 37 oder höher. Informationen zur neuesten Version des Archetyps finden Sie in der [Archetyp-Dokumentation](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=de).

+++ Microsoft® Windows

1. Öffnen Sie die Eingabeaufforderung mit Administratorrechten (führen Sie eine Eingabeaufforderung oder eine Bash-Shell als Admin aus).
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

™™™
* Legen Sie `appTitle` fest, um den Titel und die Komponentengruppen festzulegen.
* Legen Sie `appId` fest, um die Maven-Artefakt-ID (artifactId), die Namen der Komponenten-, Konfigurations- und Inhaltsordner sowie die Namen der Client-Bibliotheken festzulegen.
* Legen Sie `groupId` fest, um die Maven-Gruppen-ID (groupId) und das Java™-Quellpaket festzulegen.
* Verwenden Sie die Option `includeFormsenrollment=y` zum Einschließen von Forms-spezifischen Konfigurationen, Designs, Vorlagen, Kernkomponenten und Abhängigkeiten, die zum Erstellen adaptiver Formulare erforderlich sind.
* Durch Verwenden der Option `includeFormsheadless=y` werden Forms-Kernkomponenten und -Abhängigkeiten einbezogen, die für die Verwendung der Funktion für adaptive Headless-Formulare erforderlich sind. Wenn Sie diese Option aktivieren, sind folgende Punkte enthalten:\
* Die Vorlage **Leer mit Kernkomponenten** mit [Kernkomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=de).
* Ein Frontend-React-Modul: `ui.frontend.react.forms.af`. Es hilft Ihnen, das adaptive Headless-Formular in einer React-App zu rendern.

+++®®®


+++ Apple macOS oder Linux®

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

™™™
* Legen Sie `appTitle` fest, um den Titel und die Komponentengruppen festzulegen.
* Passen Sie `appId` an, um die Maven-Artefakt-ID (artifactId), die Komponenten-, Konfigurations- und Inhaltsordnernamen sowie die Namen der Client-Bibliotheken zu definieren.
* Legen Sie `groupId` fest, um die Maven-Gruppen-ID (groupId) und das Java™-Quellpaket festzulegen.
*  Verwenden Sie die Option `includeFormsenrollment=y` zum Einschließen von Forms-spezifischen Konfigurationen, Designs, Vorlagen, Kernkomponenten und Abhängigkeiten, die zum Erstellen adaptiver Formulare erforderlich sind.
* Durch Verwenden der Option `includeFormsheadless=y` werden Forms-Kernkomponenten und -Abhängigkeiten einbezogen, die für die Verwendung der Funktion für adaptive Headless-Formulare erforderlich sind. Wenn Sie diese Option aktivieren, sind folgende Punkte enthalten:\
* Die Vorlage **Leer mit Kernkomponenten** mit [Kernkomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=de).
* Ein Frontend-React-Modul: `ui.frontend.react.forms.af`. Es hilft Ihnen, das adaptive Headless-Formular in einer React-App zu rendern.

+++

Nach erfolgreichem Abschluss des Befehls wird ein Projektordner mit dem im `appID` angegebenen Namen erstellt. Wenn Sie beispielsweise `appID` mit dem Wert `myheadlessform` verwenden, wird ein Ordner mit dem Namen `myheadlessform` erstellt. Er enthält das auf dem Archetyp basierende Projekt.

### 4. Übertragen Sie das auf dem AEM-Archetyp basierende Projekt in Ihre Cloud Service-Umgebung

1. Ersetzen Sie den Inhalt des Git-Repositorys durch den Inhalt des Archetyp-basierten Projekts.

   >[!VIDEO](https://video.tv.adobe.com/v/3409809/)

1. Öffnen Sie eine Eingabeaufforderung, navigieren Sie zu Ihrem Git-Repository-Ordner und führen Sie die folgenden Befehle in der aufgelisteten Reihenfolge aus, um den ersetzten Inhalt in Ihre Cloud Service-Umgebung hochzuladen. Sie können auch einen visuellen Editor verwenden, anstatt die folgenden Befehle zum Übertragen von Inhalten in das Cloud Service-Repository zu verwenden.

   ```
      git add .
      git commit
      git push origin
   ```

### 5. Führen Sie die Build-Pipeline für Ihr Programm aus



<table style="table-layout:auto">
<tr>
  <td>
  1. Melden Sie sich bei <a href="https://experience.adobe.com/" >https://experience.adobe.com/</a> an und wählen Sie die Option <b>Experience Manager</b>.
  </td>
  <td>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program">
      <img alt="AEM as a Cloud Service-Programme" src="assets/cloud-manager-experience-manager.png">
    </a>
    <br>
  </td>
</tr>
<tr>
  <td>
  2. Klicken Sie für die Option <b>Cloud Manager</b> auf <b>Starten. </b> Eine Liste der Programme für Ihre Organisation wird angezeigt. Öffnen Sie Ihr Programm. 
  </td>
  <td>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program">
      <img alt="AEM as a Cloud Service-Programme" src="assets/cloud-manager-experience-manager-launch.png">
    </a>
    <br>
  </td>
</tr>
<tr>
  <td>
    3. Tippen Sie für Ihre Pipeline auf das Symbol „…“ und wählen Sie die Option <b>Ausführen</b>. Tippen Sie bei Aufforderung zur Ausführung der Pipeline auf <b>Ausführen</b> und warten Sie, bis der Pipeline-<b>Status</b> zu <b>Abgeschlossen</b> wechselt.  
  </td>
  <td>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/demo-add-on/create-program.html?lang=de#create-program">
      <img alt="AEM as a Cloud Service-Programme" src="assets/run-build-pipeline.png">
    </a>
    <br>
  </td>
</tr>
</table>

Jetzt ist Ihre Umgebung für adaptive Headless-Formulare bereit. Sie können jetzt die JSON-Definition eines Formulars in Ihre Cloud Service-Umgebung hochladen, ein darauf basierendes adaptives Headless-Formular erstellen und [getForm](https://opensource.adobe.com/aem-forms-af-runtime/api/#tag/Get-Form-Definition/operation/getForm) und andere Rest-APIs verwenden, um das adaptive Headless-Formular in Ihrer Anwendung oder Ihrem Dienst zu verwenden.
