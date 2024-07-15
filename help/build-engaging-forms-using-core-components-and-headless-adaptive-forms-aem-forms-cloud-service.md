---
title: Erstellen ansprechender Formulare mithilfe von Kernkomponenten und Headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Erstellen ansprechender Formulare mithilfe von Kernkomponenten und Headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
exl-id: ef99ffe9-4a37-4f0a-a4d3-78976c92220f
source-git-commit: bcc51bcae3b26cf20e7c0b5b75935bf69a991731
workflow-type: tm+mt
source-wordcount: '2452'
ht-degree: 94%

---

# Erstellen von ansprechenden Formularen mit Kernkomponenten und adaptiven Headless-Formularen in AEM Forms as a Cloud Service {#build-engaging-forms-using-core-components-and-headless}

## Labor-Übersicht {#lab-overview}

In diesem praktischen Labor lernen Sie:

Die Verwendung von AEM Forms zur einfachen Erstellung adaptiver Formulare mithilfe der neuesten Kernkomponenten, die mit AEM Sites konsistent sind, Erlebnisse für die Omni-Channel-Datenerfassung ermöglichen, indem adaptive Formulare als Headless-Formulare an Web, Mobile und Chat übermittelt werden. Außerdem lernen Sie Best Practices rund um die Formatierung, Anpassungen und Frontend-Entwicklung kennen.

## Haupterkenntnisse {#key-takeaways}

* **Geschäftliche Agilität**: Als Business-Anwenderin bzw. -Anwender kann ich mühelos Formularerlebnisse für mehrere Kanäle erstellen.

* **Unterstützung für Frontend-Entwickler**: Als Frontend-Entwicklungsperson kann ich das Anwendererlebnis mit Headless-Formularen steuern.

* **Entwicklergeschindigkeit**: Als Entwicklungsperson kann ich mühelos und konsistent Sites- und Forms-Komponenten anpassen.

## Voraussetzungen {#prerequisites}

Um dieses praktische Labor zu nutzen:

* Installieren Sie die [neueste Git-Version](https://git-scm.com/downloads). Wenn Sie mit Git noch nicht vertraut sind, lesen Sie [Git installieren](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

* Installieren Sie [Node.js 16.13.0 oder höher](https://nodejs.org/de/download/). Wenn Sie mit Node.js noch nicht vertraut sind, lesen Sie [Installationsanleitung für Node.js](https://nodejs.org/en/learn/getting-started/how-to-install-nodejs).

* [Aktivieren Sie die adaptiven Forms-Kernkomponenten](enable-headless-adaptive-forms-and-core-components-on-forms-cloud-service.md) für Ihre AEM Forms as a Cloud Service-Umgebung.

* Installieren Sie [Microsoft Visual Studio Code](https://code.visualstudio.com/download) oder einen beliebigen Text-Editor. Die Beispiele im Dokument verwenden Microsoft Visual Studio Code.



## Lektion 1 {#lesson-1}

### Ziel {#lesson-1-objectives}

Machen Sie sich mit der AEM Forms as a Cloud Service-Umgebung vertraut.

### Lektionskontext {#lesson-1-context}

In dieser Lektion lernen Sie die AEM Forms as a Cloud Service-Umgebung kennen, indem Sie in der Benutzeroberfläche navigieren.

### Übung {#lesson-1-excercise}

1. Öffnen Sie den Browser und geben Sie die URL der Autorenumgebung von Cloud Service ein. Beispiel:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Melden Sie sich bei der Authoring-Umgebung von Cloud Service an.
   ![](/help/assets/screenshot2028113829.png){width="50%" align="left"}

1. Klicken Sie auf **Formulare > Formulare und Dokumente**, um zur AEM Forms-Benutzeroberfläche zu navigieren, 



   ![](/help/assets/screenshot2028113929.png){width="50%" align="left"}

   Schließen Sie alle Popups, die sich auf Voreinstellungen oder Informationen beziehen. Alle verfügbaren Formulare werden angezeigt.


## Lektion 2

### Ziel

Erstellen Sie ein adaptives Formular mit den neuesten Kernkomponenten, konfigurieren Sie es und übermitteln Sie es.

### Lektionskontext

In dieser Lektion erstellen Sie als Business-Anwenderin oder -Anwender ein adaptives Formular für mehrere Kanäle wie Web, Mobile und Chat, indem Sie adaptive Formulare mit standardisierten OOTB-Kernkomponenten für die Datenerfassung erstellen.

### Übung

1. Erstellen Sie einen Übermittlungsendpunkt für das Formular:

   1. Öffnen Sie <https://requestbin.com/> in einer neuen Browser-Registerkarte.
   1. Klicken Sie auf **Öffentlichen Container erstellen** und kopieren Sie die Endpunkt-URL.
      ![](/help/assets/screenshot2028114329.png){width="50%" align="left"}

      ![](/help/assets/screenshot202023-03-0120at206.10.0020pm.png){width="50%" align="left"}

1. Erstellen Sie ein adaptives Formular mithilfe der Assistenten-Oberfläche:

   1. Navigieren Sie auf der in Lektion 1 verwendeten Browser-Registerkarte zur Web-Benutzeroberfläche von AEM Forms als Cloud Service und dort zu „Formulare und Dokumente“.
      ![](/help/assets/screenshot2028114029.png)

   1. Klicken Sie auf **Erstellen** und wählen Sie „Adaptives Formular“.
      ![](/help/assets/screenshot2028114629.png)

   1. Wählen Sie die Vorlage **Leer mit Kernkomponenten** aus dem Vorlagenauswahlbildschirm wie unten gezeigt:
      ![](/help/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Klicken Sie auf die Registerkarte **Stil** und wählen Sie das Design **wknd-theme** wie unten gezeigt:
      ![](/help/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Klicken Sie auf die Registerkarte **Übermittlung** , wählen Sie die Karte **An REST-Endpunkt übermitteln** aus und geben Sie den öffentlichen Papierkorb im Feld **URL für die POST-Anforderung** an, wie unten dargestellt:
      ![](/help/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Klicken Sie auf **Erstellen**. Geben Sie einen Namen und einen Titel für Ihr Formular an. Beispiel: **Registrierung**. Klicken Sie auf **Erstellen**.

   1. Der Editor für adaptive Formulare wird geöffnet. Schließen Sie alle Popups oder Dialogfelder für Voreinstellungen oder Informationen. Klicken Sie in der linken Leiste auf den Komponenten-Browser und fügen Sie **Kopfzeilen-** und **Fußzeilen**-Komponenten oben und unten in das leere Formular ein.
      ![](/help/assets/screenshot2028121929.png)

   1. Ziehen Sie Komponenten per Drag-and-Drop aus dem Komponenten-Browser, um ein Formular ähnlich dem folgenden zu erstellen:

      ![](/help/assets/screenshot2028115129.png){width="50%" align="left"}

1. Fügen Sie Validierungen zum Formular hinzu:

   1. Klicken Sie auf die **Telefonnummern**-Komponente, damit das Popup-Menü angezeigt wird. Klicken Sie im Menü auf das **Schraubensymbol**, um das Feld zu konfigurieren.

   1. Öffnen Sie die Registerkarte **Validierungen**, markieren Sie das Feld **Erforderlich**, und klicken Sie auf **Fertig**. Die Erfolgsmeldung wird angezeigt.
      ![](/help/assets/screenshot2028123529.png){width="50%" align="left"}

      ![](/help/assets/screenshot2028123629.png){width="50%" align="left"}

1. Zeigen Sie es in der Vorschau an und senden Sie es ab.

   1. Klicken Sie auf **Vorschau**, um eine Vorschau des Formulars aus der Perspektive von Endbenutzerinnen bzw. -benutzern anzuzeigen.

   1. Füllen Sie das Formular mit Platzhalterdaten aus.

   1. Senden Sie das Formular ab.
      ![](/help/assets/screenshot2028125729.png)

   1. Überprüfen Sie in der Registerkarte „Anfrage-Container“ die gesendeten Daten.
      ![](/help/assets/screenshot2028125829.png)

1. So fügen Sie dem Formular mit Regeln Interaktivität hinzu:

   1. Klicken Sie auf die Komponente **Aktivieren Sie das Konrollkästchen, um 5 % Rabatt zu erhalten**. Klicken Sie in der Optionsleiste auf das Regel-Symbol. Es öffnet sich die Regeleditor-Option.

   1. Erstellen Sie eine Regel. Wenn die Option **Aktivieren Sie das Kontrollkästchen, um 5 % Rabatt zu erhalten** aktiviert ist, sind die Kreditkartenoptionen deaktiviert.

1. Veröffentlichen Sie das Formular.

   1. Öffnen Sie die AEM Forms-Verwaltungsoberfläche, z. B. `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`, und wählen Sie das Formular aus.

   1. Klicken Sie auf **Veröffentlichen**.

      ![](/help/assets/screenshot2028115629.png)

      Die Erfolgsmeldung wird angezeigt.

      ![](/help/assets/screenshot2028115729.png)

      Die Veröffentlichungs-URL des Formulars ähnelt `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

   1. Ersetzen Sie zum Anzeigen des veröffentlichten Formulars die Programm-ID (pXXXXXX) und die Umgebungs-ID (eXXXXXX) in der obigen URL durch die IDs Ihrer 
Umgebung.

## Lektion 3

### Ziel

Aktualisieren Sie Stile mithilfe der Best Practices für die Frontend-Entwicklung.

### Lektionskontext

In dieser Lektion erfahren Sie als Frontend-Entwicklungsperson, wie Sie die Formatierung für das zuvor erstellte adaptive Formular einfach aktualisieren können.

### Übung

Richten Sie ein lokales Repository des Designs ein:

1. Öffnen Sie die Eingabeaufforderung oder Shell mit Administratorrechten:

   ![](/help/assets/screenshot2028115829.png){width="50%" align="left"}

1. Verwenden Sie in der Eingabeaufforderung den folgenden Befehl, um zum Ordner **c:\git** zu navigieren

   ```Shell
   cd c:\git
   ```

1. Verwenden Sie den folgenden Befehl, um den Frontend-Code des Designs zu klonen:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Verwenden Sie den folgenden Befehl in der angegebenen Reihenfolge, um zum Verzeichnis **aem-forms-theme-canvas** zu navigieren und Visual Studio Code zu öffnen.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/assets/screenshot2028126029.png)

1. Wählen Sie **Trust the authors of all files in the parent folder** und klicken Sie auf **Yes, I trust the authors**.

   ![](/help/assets/screenshot2028116229.png){width="50%" align="left"}

1. Um das in der Publishing-Umgebung Ihres Cloud-Service gehostete Formular wiederzugeben, benennen Sie die Datei `env_template` um. Um die Datei umzubenennen, klicken Sie mit der rechten Maustaste auf die Datei **env_template** und wählen Sie die Option **Umbenennen**.

   ![](/help/assets/screenshot2028116429.png){width="50%" align="left"}

   </br>

   ![](/help/assets/screenshot2028116529.png){width="50%" align="left"}

1. Legen Sie die folgenden Werte für die Variablen in der .env-Datei fest und speichern Sie die Datei:

   * **AEM_URL**: Geben Sie die Publishing-Umgebung Ihres Cloud-Service an. Beispiel: `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**: Geben Sie den Pfad des Formulars an. Wenn der Formularpfad beispielsweise `/content/forms/af/registration` ist, würde der Wert dieser Variablen `registration` sein.

     ![](/help/assets/screenshot2028116429.png){width="50%" align="left"}

1. Erstellen Sie einen lokalen Benutzer in AEM Umgebung.

   >[!NOTE]
   > So erstellen Sie eine lokale Benutzerin oder einen lokalen Benutzer:
   > Gehe zu `AEM Home` > `Tools` > `Security` > `Users`
   > Stellen Sie sicher, dass der Benutzer Mitglied der Gruppe &quot;forms-users&quot;ist.


1. Führen Sie im Eingabeaufforderungsfenster den folgenden Befehl aus:

   ```Shell
   npm install
   ```

   ![](/help/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Wenn Sie eine Meldung erhalten, in der Sie aufgefordert werden, npm über den Befehl `npm notice Run npm nstall -g npm@9.6.0` zu aktualisieren, ignorieren Sie die Nachricht.
   > * Führen Sie keine anderen npm-Befehle aus, es sei denn, Sie werden dazu in der Arbeitsmappe angewiesen.

1. Führen Sie nun den folgenden Befehl aus, um eine Vorschau des Formulars anzuzeigen.

   ```Shell
   npm run live
   ```

   ![](/help/assets/screenshot2028117229.png)

   Warten Sie nach Ausführung des oben genannten Befehls auf die Meldung `webpack compiled` und Sie werden zu einer AEM Anmeldeseite umgeleitet.

1. Klicken Sie auf der AEM Anmeldeseite auf **Lokal anmelden (nur Admin-Aufgaben)** .
1. Geben Sie die Anmeldedaten für den erstellten lokalen Benutzer ein und das Formular wird auf einer Browser-Registerkarte angezeigt.

   >[!NOTE]
   >
   >Wenn nach der Ausführung des Befehls `npm run live` für mehr als 3–4 Minuten ein leerer Browser-Bildschirm erscheint, ändern Sie `localhost` in der Browser-URL zu 127.0.0.1 und betätigen Sie die **Eingabetaste**.


   ![](/help/assets/screenshot2028115129.png){width="50%" align="left"}


1. Öffnen Sie in Visual Studio Code die Datei `PROJECT\src\site\_variables.scss`. Beachten Sie, dass die Farbe `$error` ein Farbton von ROT ist.

   ![](/help/assets/screenshot2028120729.png){width="50%" align="left"}

1. Übermitteln Sie das Formular im Browser, um die rote Farbe im Feld **Vorname** zu sehen.

   ![](/help/assets/screenshot2028120829.png)

1. Legen Sie die Farbe für **$error** auf **#5736eb** fest und speichern Sie die Datei.

   ![](/help/assets/screenshot2028120729.png){width="50%" align="left"}

1. Aktualisieren Sie den Browser und übermitteln Sie das Formular. Sie sehen, dass sich die Fehlerfarbe im Vorname-Feld entsprechend geändert hat.

   ![](/help/assets/screenshot2028121129.png)

1. Drücken Sie in der Eingabeaufforderung **Strg+C**, geben Sie **Y** ein und drücken Sie die **Eingabetaste** zum Beenden des npm-Prozesses. Es ist wichtig, den npm-Server anzuhalten, damit er nicht mit dem nächsten Satz von Übungen in Konflikt gerät.
1. Schließen Sie Visual Studio Code und das Eingabeaufforderungsfenster.

## Lektion 4

### Ziel

Rendern Sie das Formular auf Web-/Mobile- und anderen Benutzeroberflächen als Headless-Formular.

### Lektionskontext

In dieser Lektion erfahren Sie als Frontend-Entwicklungsperson, wie Sie das zuvor erstellte adaptive Formular mithilfe des React-Spektrum-Design-Frameworks als Headless-Formular rendern können.

### Übung

Richten Sie ein lokales Repository mithilfe des React-Starter-Projekts ein:

1. Öffnen Sie die Eingabeaufforderung mit Administratorrechten.

   ![](/help/assets/screenshot2028115829.png){width="50%" align="left"}

1. Verwenden Sie in der Eingabeaufforderung den folgenden Befehl, um zum Ordner **c:\git** zu navigieren

   ```Shell
   cd c:\git
   ```

1. Verwenden Sie den folgenden Befehl, um das React-Starter-Projekt des adaptiven Formulars zu klonen:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/assets/screenshot2028117329.png)

1. Verwenden Sie die folgenden Befehle in der angegebenen Reihenfolge, um zum Verzeichnis **react-starter-kit-aem-headless-forms** zu navigieren, und öffnen Sie Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/assets/screenshot2028117529.png)


   Das Fenster „Visual Studio Code“ wird geöffnet.

   ![](/help/assets/screenshot2028117429.png){width="50%" align="left"}

So rendern Sie das in der Publishing-Umgebung Ihres Cloud-Service gehostete Formular:

1. Benennen Sie die Datei „env_template“ in eine Datei „.env“ um. Klicken Sie zum Umbenennen mit der rechten Maustaste auf die Datei **env_template** und wählen Sie die Option **Umbenennen**.

   ![](/help/assets/screenshot2028117629.png){width="50%" align="left"}

   ![](/help/assets/screenshot2028117729.png)

1. Legen Sie die folgenden Werte für die Variablen in der .env-Datei fest. Speichern Sie die Datei nach dem Aktualisieren der Variablen.

   * **AEM_URL**: Geben Sie die URL der Publishing-Umgebung des Cloud-Service an. Beispiel: `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**: Geben Sie den Pfad des adaptiven Formulars an, das in der vorherigen Lektion erstellt wurde. Beispiel: `/content/forms/af/registration/`

     ![](/help/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Öffnen Sie das Befehlsfenster, stellen Sie sicher, dass Sie sich im Verzeichnis „react-starter-kit-aem-headless-forms“ befinden, und führen Sie den folgenden Befehl aus:

   ```Shell
   npm install
   ```

   ![](/help/assets/screenshot2028118029.png)


1. Führen Sie im Eingabeaufforderungsfenster den folgenden Befehl aus:

   ```Shell
   npm start
   ```

   ![](/help/assets/screenshot2028118129.png)

   Der obige Befehl startet einen lokalen Entwicklungs-Server, der die von AEM abgerufene Formulardefinition mithilfe der Frontend-Bibliothek von React Spectrum auf eine Headless-Weise rendert.

   >[!NOTE]
   >
   > 
   > Wenn nach der Ausführung des Befehls `npm start` für mehr als 3–4 Minuten ein leerer Browser-Bildschirm erscheint, ändern Sie `localhost` in der Browser-URL zu 127.0.0.1 und drücken Sie die **Eingabetaste**.

   ![](/help/assets/screenshot2028118229.png)

Überprüfen wir die Ausführung der Regeln in diesem Headless-Formular:

1. Wählen Sie die Option **Aktivieren Sie das Kontrollkästchen, um 5 % Rabatt zu erhalten**. Die nachfolgende Option zum Anwenden einer Kreditkarte ist deaktiviert.

   ![](/help/assets/screenshot2028126229.png)

1. Heben Sie die Option **Aktivieren Sie das Kontrollkästchen, um 5 % Rabatt zu erhalten** auf, um die Kreditkartenoption zu aktivieren.

   ![](/help/assets/screenshot2028126329.png)

Jetzt nehmen wir als Business-Anwenderin bzw. -Anwender Änderungen am Formular auf dem Server vor und zeigen die Änderungen automatisch im Headless-Formular an.

1. Öffnen Sie die AEM Forms-Verwaltungsoberfläche im Browser. Zum Beispiel [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Öffnen Sie das Formular **Kontakt** und klicken Sie auf **Bearbeiten.** Das Formular wird im Editor für adaptive Formulare geöffnet.


1. Wählen Sie das Feld **Telefonnummer** und klicken Sie auf das **Symbol „Bearbeiten“ (Bleistiftsymbol)** in der Symbolleiste. Wenn Sie die Popup-Symbolleiste nicht sehen können, wechseln Sie in den Bearbeitungsmodus, indem Sie auf die Schaltfläche **Bearbeiten** oben rechts, links von der Schaltfläche **Vorschau**, klicken.

   ![](/help/assets/screenshot2028119629.png)

1. Ändern Sie die Beschriftung in „Mobiltelefonnummer“. Klicken Sie auf eine leere Stelle im Formular, damit die am Formular vorgenommenen Änderungen gespeichert werden.

   ![](/help/assets/screenshot2028119729.png)

Veröffentlichen wir das aktualisierte Formular, um die Änderungen in die Publishing-Umgebung zu übertragen.

1. Wählen Sie in der Registerkarte der Verwaltungsoberfläche von AEM Forms das Registrierungsformular aus und klicken Sie auf **Veröffentlichung rückgängig machen**. Wenn Sie die Schaltfläche **Veröffentlichung rückgängig machen** nicht sehen, fahren Sie mit Schritt 3 fort, um die Änderungen direkt zu veröffentlichen.

1. Klicken Sie auf **Veröffentlichung aufheben**. Klicken Sie auf **Schließen** im entsprechenden Dialogfeld.

1. Nachdem der Browser aktualisiert wurde, wählen Sie das Registrierungsformular aus und klicken Sie auf **Veröffentlichen**.

1. Klicken Sie auf **Veröffentlichen**. Klicken Sie auf **Schließen** im entsprechenden Dialogfeld.

1. Aktualisieren Sie die Browser-Registerkarte mit dem angezeigten Headless-Formular. Beachten Sie, dass die Beschriftung für die Telefonnummer in „Mobiltelefonnummer“ geändert wurde.

   ![](/help/assets/screenshot2028120529.png)

1. Öffnen Sie das Eingabeaufforderungsfenster, das zum Starten des Projekts **react-starter-kit-aem-headless-forms** genutzt wird, drücken Sie **Strg+C**,
geben Sie **Y** ein und drücken Sie die Eingabetaste, um den npm-Prozess zu beenden. Es ist wichtig, den npm-Server anzuhalten, damit er nicht mit dem nächsten Satz von Übungen in Konflikt gerät.

1. Schließen Sie Visual Studio Code und das Eingabeaufforderungsfenster.


## Lektion 5

### Ziel

Rendern des Formulars als Headless-Formular mithilfe der Google Material-Benutzeroberfläche

### Lektionskontext

In dieser Lektion erfahren Sie als Frontend-Entwicklerperson, wie Sie das zuvor erstellte adaptive Formular mithilfe der Google Material-Benutzeroberfläche als Headless-Formular wiedergeben.

### Übung

Richten Sie das lokale Repository mithilfe des Ausgangsprojekts der Material-Benutzeroberfläche ein:

1. Öffnen Sie die Eingabeaufforderung mit Administratorrechten.

   ![](/help/assets/screenshot2028115829.png){width="50%" align="left"}


1. Verwenden Sie in der Eingabeaufforderung den folgenden Befehl, um zum Ordner **c:\git** zu navigieren:

   ```Shell
   cd c:\git
   ```

1. Führen Sie die folgenden Befehle in der angegebenen Reihenfolge aus, um einen Ordner mit dem Namen „mui“ zu erstellen und zu diesem Ordner zu navigieren:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Verwenden Sie den folgenden Befehl, um das React-Starter-Projekt des adaptiven Formulars zu klonen:

   ```Shell
   git clone -b mui-lab https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/assets/screenshot2028126529.png)

1. Verwenden Sie die folgenden Befehle in der aufgeführten Reihenfolge, um zum Ordner **react-starter-kit-aem-headless-forms** zu navigieren und den Code in Visual Studio Code zu öffnen:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/assets/screenshot2028126829.png)

So rendern Sie das in der Publishing-Umgebung Ihres Cloud-Service gehostete Formular:

1. Benennen Sie die Datei **env_template** in eine Datei **.env** um. Klicken Sie zum Umbenennen mit der rechten Maustaste auf die Datei **env_template** und wählen Sie **Umbenennen**.

   ![](/help/assets/screenshot2028126629.png){width="50%" align="left"}

1. Legen Sie die folgenden Werte für die Variablen in der .env-Datei fest. Speichern Sie die Datei nach dem Aktualisieren der Variablen. Verwenden Sie die Tastenkombination **Strg+S**, um die Datei zu speichern.

   * **AEM_URL**: Geben Sie die URL der Publishing-Umgebung des Cloud-Service an. Beispiel: [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: Geben Sie den Pfad des adaptiven Formulars an, das in der vorherigen Lektion erstellt wurde. Beispiel: /content/forms/af/registration/

     ![](/help/assets/screenshot2028126929.png)

1. Öffnen Sie das Befehlsfenster, stellen Sie sicher, dass Sie sich im Verzeichnis **react-starter-kit-aem-headless-forms** befinden, und führen Sie den folgenden Befehl aus:

   ```Shell
   npm install
   ```

   ![](/help/assets/screenshot2028127029.png)

1. Führen Sie im Eingabeaufforderungsfenster den folgenden Befehl aus:

   ```Shell
   npm start
   ```

   ![](/help/assets/screenshot2028127129.png)

   Der Befehl startet einen lokalen Entwicklungs-Server und rendert die von AEM abgerufene Formulardefinition mithilfe der 
Frontend-Bibliothek der Google Material-Benutzeroberfläche auf eine Headless-Weise.

   >[!NOTE]
   >
   >Wenn nach der Ausführung des Befehls `npm start` für mehr als 3–4 Minuten ein leerer Browser-Bildschirm erscheint, ändern Sie `localhost` in der Browser-URL zu 127.0.0.1 und drücken Sie die **Eingabetaste**

   ![](/help/assets/screenshot2028127229.png)

1. So bewerten Sie die Ausführung derselben Business-Logik in dieser Formularausgabedarstellung:

   Wählen Sie **Aktivieren Sie das Kontrollkästchen, um 5 % Rabatt zu erhalten**. Die nachfolgende Option **Möchten Sie das We.Finance Corporate Kreditkarten-Formular beantragen?** wird deaktiviert.

   ![](/help/assets/screenshot2028127329.png){width="50%" align="left"}

## Lektion 6

### Ziel

Erstellen Sie ein alternatives Look-and-Feel des Headless-Formulars mithilfe der Komponentenvarianten der Material-Benutzeroberfläche

### Lektionskontext

In dieser Lektion erfahren Sie als Frontend-Entwicklungsperson, wie Sie mithilfe der Material-Benutzeroberfläche eine alternative Darstellung verschiedener Komponenten für das adaptive Formular erstellen, das zuvor von einer Business-Anwenderin oder einem -Anwender erstellt wurde.

### Übung

Aktualisieren Sie die Variation der Komponenten im Headless-Projekt. So ändern Sie die Variante der Texteingabekomponente der materiellen Benutzeroberfläche in `OutlinedInput`:

1. Navigieren Sie in Visual Code zur Texteingabekomponente, indem Sie die Datei `index.tsx` unter `src/components/textinput/index.tsx` öffnen.

1. Fügen Sie `//` am Anfang der Code-Zeile 103 hinzu. Die Zeile wird dadurch in einen Kommentar umgewandelt.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Fügen Sie in Zeile 104 Folgendes hinzu, um eine andere Variante der Komponente zu verwenden und die Datei zu speichern. Verwenden Sie die Tastenkombination **Strg+S**, um die Datei zu speichern.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/assets/screenshot2028127629.png)

   Es ist wichtig, die richtige Groß-/Kleinschreibung für die Variante „OutlinedInput“ zu verwenden, da die Kompilierung andernfalls fehlschlagen würde. Die Kompilierung der lokalen Entwicklungsumgebung beginnt automatisch in der Eingabeaufforderung. Warten Sie, bis die folgende Meldung angezeigt wird

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Aktualisieren Sie den Browser, wenn er nicht automatisch aktualisiert wird, um zu sehen, wie die Texteingabe-Komponente eine andere Variante verwendet.

   ![](/help/assets/screenshot2028127729.png)


   Diese Änderung erfolgt für Endbenutzerinnen und -benutzer ohne Änderung der Formulardefinition auf dem AEM Forms-Server und ist spezifisch für den betreffenden Headless-Kanal. Beispiel: Web-Kanal in diesem Labor.

   ![](/help/assets/screenshot2028127529.png){width="50%" align="left"}


1. Schließen Sie Visual Studio Code und das Eingabeaufforderungsfenster.

## Häufig gestellte Fragen (FAQs)

+++ Ist der Assistent für adaptive Formulare öffentlich verfügbar?

Ja, er ist mit AEM Forms as a Cloud Service verfügbar.

+++


+++ Sind Kernkomponenten öffentlich verfügbar?

Ja, die Kernkomponenten der adaptiven Formulare sind mit AEM Forms as a Cloud Service verfügbar.

+++

+++ Sind Headless-Formulare öffentlich verfügbar?

Ja, Headless-Formulare sind mit AEM Forms as a Cloud Service verfügbar.

+++

+++ Benötigen Headless-Formulare eine separate Lizenz?

Nein, Headless-Formulare verwenden dieselbe Metrik für den Lizenzwert, nämlich die Anzahl der Formularübertragungen.

+++

+++ Sind Kernkomponenten und Headless-Formulare in AEM 6.5 Forms verfügbar?

Ja, sowohl Kernkomponenten für adaptive Formulare als auch Headless-Formulare sind mit AEM Forms 6.5 Service Pack 16 und höher verfügbar.

+++


## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie adaptive Formulare erstellen und über Headless-Formulare an mehrere Kanäle senden, sollten Sie versuchen, Ihre neuen Fähigkeiten in die Tat umzusetzen. Viel Spaß beim Erstellen und Bereitstellen von umfangreichen, außergewöhnlichen Datenerfassungserlebnissen für Ihre Endbenutzerinnen und -benutzer, wo auch immer sie sich befinden!

## Ressourcen

* [Einführung zu Kernkomponenten für adaptive Formulare](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=de)

* [Erstellen eines adaptiven Formulars mit Kernkomponenten](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=de)

* [Aktualisierungsstile für die auf Kernkomponenten basierenden adaptiven Formulare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=de)

* [Adaptive Headless-Formulare](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=de)

* [Verwenden des Headless-React-Starter-Kits](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=de)
