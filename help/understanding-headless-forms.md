---
title: Grundlegendes zu Headless-Formularen - Konzepte und häufig gestellte Fragen
description: Antworten auf häufige Fragen dazu, was Headless-Formulare sind und wie sie sich von herkömmlichen Formularbibliotheken unterscheiden, sowie Implementierungsdetails, Benutzeroberflächensteuerung, Leistung und Integration mit Frameworks und Backends.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
keywords: Headless-Formulare, Headless-Formularbibliothek, adaptive Formulare, Statusverwaltung, Validierung, Design-System, SSR, CMS
index: true
exl-id: 539da3e9-25c5-4e26-ba4e-f68cf849bca4
source-git-commit: 86129488bec7faed87600a237ac034ca1b601187
workflow-type: tm+mt
source-wordcount: '2605'
ht-degree: 5%

---

# Grundlegendes zu Headless-Formularen - Konzepte und häufig gestellte Fragen {#understanding-headless-forms}

Dieses Handbuch beantwortet häufige Fragen zu Headless-Formularen im Allgemeinen und dazu, wie sie auf AEM Headless Adaptive Forms angewendet werden. Verwenden Sie ihn, um zu entscheiden, wann ein Headless-Ansatz verwendet werden soll und wie Formulare in Ihren Stack implementiert, formatiert und integriert werden sollen.

## Grundlagen und Verständnis {#basics-understanding}

### Was genau ist eine Headless-Formular-Bibliothek?

Eine **Headless-**&quot; ist eine Formularlösung, die **Formularlogik** (Status, Validierung, Regeln, Übermittlung) von **Präsentation)** (UI-Komponenten und Stile) trennt. Der „Kopf“ ist die Benutzeroberfläche des sichtbaren Formulars. „Headless“ bedeutet, dass die Bibliothek keine feste Benutzeroberfläche vorgibt oder bereitstellt. Stattdessen wird Folgendes verfügbar gemacht:

* Ein **Formularmodell** (häufig JSON): Struktur, Felder, Einschränkungen und Regeln.
* **APIs oder Hooks** zum Lesen und Aktualisieren des Formularstatus, Ausführen der Validierung und Verarbeiten der Übermittlung.
* **Ereignisse und Lebenszyklus** sodass Ihre Benutzeroberfläche auf Änderungen reagieren kann.

In AEM Headless Adaptive Forms ist das Formular eine [JSON-Struktur](architecture.md) die auf Adobe Experience Manager gehostet wird. Die [Forms Web SDK](architecture.md#developer-tools) (Client-seitige Laufzeit) stellt die Logikschicht bereit - Geschäftsregelprozessor, Statusverwaltung, Validierung -, während Ihre App die Benutzeroberfläche bereitstellt, die diese Struktur rendert.

### Wie unterscheidet sich ein Headless-Formular von einer herkömmlichen Formularbibliothek?

| Aspekt | Bibliothek für herkömmliche Formulare | Headless-Formularbibliothek |
|--------|---------------------------|------------------------|
| **UI** | Im Lieferumfang enthalten sind integrierte Komponenten und Stile | Keine vorgeschriebene Benutzeroberfläche; Sie bringen Ihre eigenen Komponenten mit |
| **Stile** | Designs oder Überschreibungen für Bibliothekskomponenten | Vollständige Kontrolle; verwenden Sie Ihr Designsystem wie es ist |
| **Formulardefinition** | Häufig nur Code (Komponenten in JSX/HTML) | Häufig datengesteuert (JSON/Schema aus CMS oder API) |
| **Status und Validierung** | An Bibliothekskomponenten gebunden | Wird über APIs/Hooks bereitgestellt; jede Benutzeroberfläche kann daran gebunden werden |
| **Kanäle** | Normalerweise Web (manchmal ein Framework) | Dieselbe Formulardefinition kann für Web, Mobilgeräte, Chat usw. verwendet werden. |

Mit AEM Headless Adaptive Forms [&#x200B; Sie (ein Formular erstellen und &#x200B;](create-and-publish-a-headless-form.md)) einmal in AEM veröffentlichen. Jeder Client (React, Angular, Native Mobile, Chatbot) kann [&#x200B; Formular-JSON abrufen &#x200B;](architecture.md) mit der entsprechenden Benutzeroberfläche für diesen Kanal rendern.

### Warum sollte ich Headless-Formulare anstelle einer auf der Benutzeroberfläche basierenden Formularlösung verwenden?

Headless-Formulare eignen sich gut, wenn Sie Folgendes benötigen:

* **Systemkonsistenz gestalten** - Verwenden Sie Ihre vorhandenen Komponenten und Marken, ohne die Bibliotheksstandardwerte zu verändern.
* **Multi-Channel** - Eine Formulardefinition für Web, Mobile und andere Touchpoints (siehe [Übersicht](overview.md)).
* **CMS- oder Backend-gesteuerte Formulare** - Autoren ändern die Formularstruktur und die Regeln, ohne dass Code bereitgestellt wird. Ihre App nutzt nur die JSON-Datei.
* **Framework-**: Die [AF-core](https://www.npmjs.com/package/@aemforms/af-core)-Bibliothek ist Framework-unabhängig. React-Bindungen werden aus praktischen Gründen bereitgestellt, Sie können jedoch Bindungen für andere Frameworks erstellen.
* **Backend-Funktionen** - Nutzen Sie AEM Forms für Vorbefüllung, Validierung, Übermittlung, Workflows und das Forms-Datenmodell, ohne sich an einen bestimmten UI-Stack zu binden.

### Wann ist es sinnvoll, einen Headless-Ansatz zu verwenden?

Verwenden Sie Headless-Formulare, wenn:

* Sie haben oder möchten ein starkes Design-System oder eine starke Komponentenbibliothek.
* Forms werden von Nicht-Entwicklern verfasst (z. B. in einer CMS) und müssen über mehrere Apps oder Kanäle hinweg funktionieren.
* Sie benötigen dieselbe Formularlogik (Validierung, Regeln) für Web-, Mobile- oder andere Clients.
* Sie möchten das erneute Rendern minimieren und die Formularlogik unabhängig von der Benutzeroberfläche testbar halten.

Stellen Sie sich eine herkömmliche, in der Benutzeroberfläche enthaltene Formularbibliothek vor, wenn Sie:

* Sie benötigen schnell ein Arbeitsformular in einer einzelnen Web-Anwendung und interessieren sich nicht für benutzerdefinierte Benutzeroberfläche oder Multi-Channel.
* Ihr Team zieht es vor, Formulare nur in Code in einem Framework zu definieren.

### Ist „Headless“ nur ein Schlagwort oder löst es echte Probleme?

Es löst echte architektonische Probleme:

* **Trennung von Belangen** - Formularstruktur, Regeln und Validierung live in Daten und einer logischen Ebene. Die Benutzeroberflächenebene rendert nur und sendet Benutzeraktionen. Dies verbessert die Testbarkeit und Wiederverwendung.
* **Kanalunabhängigkeit** - Eine Formulardefinition kann verschiedene Benutzeroberflächen steuern (z. B. React Web, React Native, Angular oder Voice). AEM Headless Adaptive Forms wurden für Folgendes erstellt: [Einmal erstellen, über React, SPAs, Web, Mobile und mehr bereitstellen](overview.md).
* **Authoring ohne Code** - Business-Anwender können Felder und Regeln im [Editor für adaptive Formulare](create-a-headless-adaptive-form.md) ändern. Entwickler müssen sie für Inhaltsänderungen nicht erneut bereitstellen.
* **Integration mit vorhandenen Stacks** - Sie behalten Ihr Design-System, die Statusverwaltung und das Routing bei; die Headless-Ebene verwaltet nur den Formularstatus, die Validierung und die Übermittlung.

## Implementierungs- und technische Fragen {#implementation-technical}

### Wie verwalten Headless-Formulare den Status?

In AEM Headless Adaptive Forms wird der Status von der **Forms Web SDK verwaltet**:

* **Geschäftsregelprozessor** - Akzeptiert das Formular-JSON, verwaltet den Feldstatus und führt die im JSON definierten Regeln und Ereignis-Handler aus.
* **React Binder** - Stellt Hooks (z. B. `useRuleEngine`) über den Controller bereit, sodass React-Komponenten den aktuellen Status und Handler erhalten. Derselbe Status kann von Nicht-React-Benutzeroberflächen über die Kern-APIs genutzt werden.
* **Status** umfasst Feldwerte, Sichtbarkeit, Gültigkeit und alle benutzerdefinierten Eigenschaften, die im Formularmodell definiert sind.

Ihre UI-Komponenten erhalten Status und Handler (z. B. `[state, handlers] = useRuleEngine(props)`). Sie werden aus `state` gerendert und rufen `handlers` auf, wenn der Benutzer interagiert. Der Laufzeitstatus bleibt mit der Formulardefinition und den Regeln synchronisiert. Siehe [Architektur](architecture.md) und [Verwenden benutzerdefinierter Komponenten zum Rendern eines Headless-Formulars](developing-for-headless-forms-using-your-own-components.md).

### Wie funktioniert die Validierung in einer Headless-Formular-Einrichtung?

Die Validierung ist Teil der Formularlogikschicht:

* **Beschränkungen** werden in der Formular-JSON definiert (z. B. erforderlich, min/max, Muster). Forms Web SDK wendet diese Einschränkungen an und stellt den Validierungsstatus (z. B. gültige/ungültige Fehlermeldungen) für Ihre Komponenten zur Verfügung.
* **Client-seitige Validierung** wird von der SDK basierend auf der Formularstruktur angewendet. Ihre Benutzeroberfläche zeigt Statusfehler an.
* **Server-seitige Validierung** ist über AEM-APIs (z. B. den Validate-Endpunkt) verfügbar; Sie können vor oder während des Übermittlens überprüfen.

Sie implementieren keine Validierungslogik in Ihrer Benutzeroberfläche - Sie zeigen nur den Validierungsstatus und die von der Laufzeit bereitgestellten Meldungen an.

### Kann ich Headless-Formulare mit Schemavalidierung integrieren (Jup, Zod, Join)?

Die integrierte Validierung wird von den JSON-Einschränkungen des Formulars gesteuert. So verwenden Sie Yup, Zod, Joi oder Ähnliches:

* Sie können **Headless-JSON für** adaptive Formular von Ihrem Schema ableiten oder generieren (z. B. JSON-Schema in Formular-JSON konvertieren), sodass eine Datenquelle sowohl die Schemavalidierung als auch die Formularstruktur steuert.
* Für **benutzerdefinierte Validierung** jenseits des Formular-JSON können Sie Ihre eigenen Validatoren (Yup/Zod/Joi) in Ereignis-Handlern oder vor dem Senden ausführen und Ergebnisse in den Formularstatus oder die Blockübermittlung pushen. Integrationspunkte sind dieselben Hooks/APIs, die Sie für den Status und die Übermittlung verwenden.

Die [Spezifikation für adaptive Forms](/help/assets/headless-adaptive-forms-specification.pdf) und [JSON-Formel](architecture.md) definieren das Regel- und Einschränkungsmodell, das von der Laufzeit verwendet wird.

### Wie handhabe ich die asynchrone Validierung (z. B. die Verfügbarkeit von Benutzernamen)?

Asynchrone Validierung kann auf Anwendungsebene implementiert werden:

* Verwenden Sie **Regeln oder Ereignis-Handler** in der Formular-JSON (sofern unterstützt), um die Logik beim Ändern eines Triggers zu ändern.
* Verwenden Sie in **benutzerdefinierten Komponenten** Status-/Handler-Hooks, um Ihr Backend aufzurufen (z. B. die API zur Benutzernamenverfügbarkeit), aktualisieren Sie dann die Gültigkeit des Felds oder zeigen Sie über die Laufzeit-APIs oder den lokalen Status, den Sie in der Benutzeroberfläche anzeigen, einen Fehler an.
* Alternativ können Sie die Prüfung **on blur oder before submit** durchführen und den Feldstatus mit einer benutzerdefinierten Meldung auf ungültig setzen, wenn die asynchrone Prüfung fehlschlägt.

Das genaue Muster hängt davon ab, wie Ihre App mit dem [Geschäftsregelprozessor) &#x200B;](architecture.md) benutzerdefinierten Komponenten integriert wird.

### Wie sende ich Daten mithilfe von Headless-Formularen an APIs?

Die Übermittlung wird von der Benutzeroberfläche entkoppelt:

* **AEM-Übermittlungsaktionen** - Sie konfigurieren das Formular in AEM so, dass es an REST-Endpunkte, E-Mail oder Integrationen (z. B. Microsoft Dynamics, Salesforce) gesendet wird. Das Formular wird über AEM übermittelt, das den eigentlichen HTTP/Backend-Aufruf verarbeitet. Siehe [Verwenden von Ereignissen zum Verarbeiten und Senden von &#x200B;](use-events-to-handle-and-submit-form-data.md)).
* **Client-seitiges Senden** - Ihre App kann auf gesendete oder erfasste Formulardaten aus dem Laufzeitstatus warten und sie an Ihre eigenen APIs senden. Mit [HTTP-APIs](https://opensource.adobe.com/aem-forms-af-runtime/api/) wird der Übermittlungsstatus aufgelistet, abgerufen, validiert, gesendet und verfolgt.
* **Vorbefüllen** - Daten können über REST-Endpunkte oder Server-seitig vorbefüllt werden, sodass der Status beim Laden des Formulars bereits ausgefüllt ist. Siehe [Storybook - Beispiel zum Vorbefüllen](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-examples--prefill-form-with-personalised-data).

## Benutzeroberfläche und Design-Steuerung {#ui-design-control}

### Kann ich mein eigenes Design-System oder meine eigene Komponentenbibliothek mit Headless-Formularen verwenden?

Ja. Dies ist ein wesentlicher Vorteil von Headless-Formularen. Mit AEM Headless Adaptive Forms:

* Sie **dem** (nach Feldtyp oder Ressourcentyp) Ihre eigenen Komponenten zuordnen. Siehe [Verwenden benutzerdefinierter Komponenten zum Rendern eines Headless-Formulars](developing-for-headless-forms-using-your-own-components.md) und [Verwenden von React-Komponenten der Google Material-Benutzeroberfläche zum Rendern eines Headless-Formulars](use-google-material-ui-react-components-to-render-a-headless-form.md).
* Die Laufzeit stellt **Status und Handler** bereit. Ihre Komponenten werden mithilfe Ihres Designsystems gerendert und die Handler werden aufgerufen, damit die Formularlogik synchron bleibt.
* Sie können **React Spectrum**, Material UI, Chakra UI oder eine beliebige benutzerdefinierte Komponentenbibliothek verwenden. Die [Spezifikation](/help/assets/headless-adaptive-forms-specification.pdf) kann für benutzerdefinierte Komponenten (z. B. Chakra UI, Vue.js) erweitert werden. Siehe [FAQ - Benutzerdefinierte Frameworks](faq.md#is-it-possible-to-use-headless-adaptive-forms-with-custom-frameworks).

### Bieten Headless-Formulare Barrierefreiheitsunterstützung (ARIA, Tastaturverarbeitung)?

Die Barrierefreiheit wird in der von **bereitgestellten UI** Ebene implementiert. Die Headless-Ebene rendert kein DOM, sodass sie kein ARIA- oder Tastaturverhalten von sich aus hinzufügt. Sie erhalten Barrierefreiheit durch:

* Verwendung **barrierefreien Komponenten** aus Ihrem Design-System oder Ihrer Bibliothek (viele umfassen ARIA- und Tastaturunterstützung).
* Befolgen Sie **Best Practices zur Barrierefreiheit** in Ihren benutzerdefinierten Feldkomponenten (Beschriftungen, Fehlermeldungen, Fokusverwaltung, Tastaturnavigation).
* Sicherstellen, dass die Formularstruktur und der Status, die Sie erhalten (z. B. erforderlich, ungültig, sichtbar) in den ARIA-Attributen und im Verhalten Ihrer Komponenten berücksichtigt werden.

Wenn Sie die vorkonfigurierten Komponenten auf Basis von React Spectrum verwenden, profitieren Sie von der integrierten Barrierefreiheit.

### Wie handhabe ich komplexe UI-Komponenten (Datumsauswahl, benutzerdefinierte Dropdown-Listen)?

Behandeln Sie sie als **benutzerdefinierte Komponenten**, die den entsprechenden Feldtypen oder benutzerdefinierten Ressourcentypen im JSON-Formular zugeordnet sind:

* Implementieren Sie Ihre Komponente so, dass sie dieselben **props/state/** akzeptiert wie andere Feldkomponenten (z. B. über `useRuleEngine`).
* Verwenden Sie **state** für Wert, Sichtbarkeit und Gültigkeit; verwenden Sie **Handler**, um die Werte- und Trigger-Validierung zu aktualisieren.
* Rendern Sie die Datumsauswahl oder das benutzerdefinierte Dropdown-Menü mit der ausgewählten Benutzeroberflächenbibliothek. Rufen Sie bei einer Änderung den Handler mit dem neuen Wert auf, damit der Formularstatus korrekt bleibt.

Siehe [Verwenden benutzerdefinierter Komponenten zum Rendern eines Headless](developing-for-headless-forms-using-your-own-components.md)Formulars für die Zuordnung nach Feldtyp und Ressourcentyp.

### Kann ich Felder (dynamische Formulare) dynamisch hinzufügen oder entfernen?

Die Formularstruktur wird durch die vom Server zurückgegebene **Formular-**&quot; definiert. Dynamisches Verhalten wird erreicht durch:

* **Regeln im Formular JSON** - Werte basierend auf Ausdrücken anzeigen/ausblenden, aktivieren/deaktivieren oder festlegen. Der [Geschäftsregelprozessor](architecture.md) führt diese Regeln aus. Ihre Komponenten reagieren auf `state.visible` und Ähnliches.
* **Server-gesteuerte Struktur** - Verschiedene Benutzer oder Kontexte können unterschiedliche Formular-JSONs erhalten (z. B. verschiedene Schritte oder Abschnitte), sodass „dynamisch“ „unterschiedliche Formulardefinition pro Anfrage“ bedeuten kann.
* **Client-seitige Änderungen** - Wenn Ihre App das Formularmodell ändern kann (z. B. Elemente in einer wiederholbaren Struktur hinzufügen/entfernen), kann die Laufzeit dies widerspiegeln. Die genaue Funktion hängt vom Formularschema und von den Laufzeit-APIs ab.

Das [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/) enthält Beispiele für dynamisches Verhalten.

### Wie handhabe ich bedingte Felder (basierend auf der Eingabe ein-/ausblenden)?

Die bedingte Sichtbarkeit wird durch **Regeln** im Formular-JSON gesteuert, das vom Geschäftsregelprozessor ausgewertet wird. Sie definieren Bedingungen (z. B. „wenn Feld A gleich X ist, Feld B anzeigen„); der Laufzeitstatus wird aktualisiert (z. B. `state.visible`). Ihre Komponenten müssen nur **Status respektieren** (z. B. `if (!state.visible) return null;`). Für die Ein-/Ausblendung über das Rendern des Status hinaus ist keine zusätzliche UI-Logik erforderlich. Kaskadierendes und bedingtes Verhalten wird in der [Spezifikation für adaptive Forms](/help/assets/headless-adaptive-forms-specification.pdf) dokumentiert und in &quot;[&#x200B; - Kaskadierende Felder“ &#x200B;](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/adaptive-form-dynamic-behaviour--options&args=formJson.items[0].fieldType:drop-down;formJson.items[0].minimum:!undefined;formJson.items[0].maximum:!undefined;formJson.items[0].label.value:Choose+number+of+options;formJson.items[0].enum[0]:1;formJson.items[0].enum[1]:2;formJson.items[0].enum[2]:3;formJson.items[1].fieldType:drop-down). Siehe auch [FAQ - Kaskadierende Felder](faq.md#do-headless-adaptive-forms-support-cascading-fields).

## Leistung und Skalierbarkeit {#performance-scalability}

### Sind Headless-Formulare leistungsfähiger als herkömmliche Formularbibliotheken?

Dies ist möglich, hängt aber von der Implementierung ab:

* **Zielgerichtete Aktualisierungen** - Eine gut konzipierte Headless-Laufzeitumgebung aktualisiert nur den geänderten Status und benachrichtigt nur die davon abhängigen Komponenten, wodurch unnötige Neudarstellungen im Vergleich zu einer monolithischen Formularkomponente reduziert werden können.
* **Kleineres UI-Bundle** - Sie liefern nur die von Ihnen verwendeten UI-Komponenten (Ihr Design-System), nicht aber einen vollständigen Satz von Bibliothekskomponenten.
* **Lazy Loading** - Formular-JSON kann bei Bedarf abgerufen werden; das anfängliche Bundle kann kleiner bleiben.

Die Leistung hängt auch davon ab, wie Sie Ihre Komponenten implementieren (z. B. Vermeidung unnötiger Rendervorgänge, Speicherung).

### Wie minimieren sie das erneute Rendern?

* **Status-**: Die Laufzeit behält den Formularstatus in einer Struktur, die feinkörnige Aktualisierungen zulässt, sodass nur betroffene Teile der Baumstruktur erneut gerendert werden müssen.
* **Hooks-Design** - Hooks wie `useRuleEngine` können implementiert werden, um Komponenten nur für den von ihnen verwendeten Status zu abonnieren, sodass übergeordnete oder gleichrangige Änderungen nicht jedes Feld zwingen, erneut zu rendern.
* **Ihre Verantwortung** - Sie können das erneute Rendern weiter minimieren, indem Sie React-Best-Practices (z. B. `React.memo`, stabile Callbacks) in Ihren benutzerdefinierten Komponenten verwenden.

### Skalieren Headless-Formulare gut für große, mehrstufige Formulare?

Ja, bei entsprechender Gestaltung:

* **Formulardefinition** - Große Formulare können in der JSON-Datei in Schritte oder Abschnitte unterteilt werden. Nur der sichtbare Schritt/Abschnitt muss möglicherweise in der Benutzeroberfläche vollständig aktiv sein, wobei die Regeln für ausgeblendete Abschnitte verzögert ausgewertet werden, falls unterstützt.
* **State**: Die Laufzeitumgebung enthält einen kohärenten Formularstatus. Bei der Schrittnavigation werden nur Abschnitte angezeigt/ausgeblendet oder der „aktuelle Schritt“ wird aktualisiert, ohne dass Daten dupliziert werden.
* **Chunking und Lazy Load** - Sie können Formular-JSON in Blöcken abrufen oder zusätzliche Abschnitte schrittweise laden, um die anfängliche Payload und die Analysekosten niedrig zu halten.

Berücksichtigen Sie bei sehr großen Formularen die Struktur (z. B. Assistentenschritte), servergesteuerte Formularvarianten und die Messung der Render- und Regelausführung mit echten Payloads.

## Integration und Ökosystem {#integration-ecosystem}

### Können Headless-Formulare mit Next.js/SSR/Server-Aktionen funktionieren?

* **Next.js / React** - Ja. Der React-Renderer und die Hooks funktionieren in einer React-Umgebung. Verwenden Sie die Forms Web SDK in Client-Komponenten. Rufen Sie Formular-JSON auf dem Server oder Client nach Bedarf ab.
* **SSR** - Sie können die Formular-JSON auf dem Server abrufen und an den Client übergeben, damit das Formular mit Daten hydriert wird. Formularinteraktivität (Status, Validierung, Regeln) wird auf dem Client ausgeführt, auf den die SDK geladen wird. Vermeiden Sie das Rendern von Formularfeldern, die während des SSR nur vom Client-Status abhängen, oder verwenden Sie einen Platzhalter, der auf dem Client hydriert.
* **Server-Aktionen (Next.js)** - Sie können Server-Aktionen über Ihren Sende-Handler aufrufen: Wenn der Benutzer sendet, erfasst Ihr Client-Code Formulardaten (aus dem Headless-Status) und ruft eine Server-Aktion anstelle von oder zusätzlich zu AEM-Sende-Endpunkten auf.

### Wie lassen sich Headless-Formulare in CMS, Headless-Commerce oder Backend-Systeme integrieren?

* **CMS** - AEM ist die CMS für die Formulardefinition: Autoren erstellen und veröffentlichen die Formular-JSON. Andere CMS können auf die Formular-URL/API verweisen oder eine Verknüpfung zu ihr herstellen. Ihre App ruft das Formular von AEM (oder einem CDN) ab und ruft optional eine Kopie oder ein Layout von einer anderen CMS ab.
* **Vorbefüllen und Senden** - [Vorbefüllen](https://opensource.adobe.com/aem-forms-af-runtime/storybook/?path=/story/reference-examples--prefill-form-with-personalised-data) und Senden kann REST-Endpunkte erreichen, sodass Sie von einem CRM-, DAM- oder Commerce-Backend vorbefüllen und an dieselben oder verschiedene Systeme senden können. AEM Forms unterstützt auch [Microsoft Dynamics und Salesforce](faq.md), REST, E-Mail und benutzerdefinierte Übermittlungsaktionen.
* **Forms-Datenmodell** - AEM Forms bietet ein Forms-Datenmodell zum Verbinden mit unterschiedlichen Datenquellen. Headless-Formulare können diese Funktionen zum Vorbefüllen, Überprüfen und Senden verwenden, ohne dass Sie selbst jede Integration erstellen müssen.

Für mobile und Offline-Szenarien wird empfohlen, [Ihre eigene App zu erstellen und Formulardefinitionen über die Headless Adaptive Forms API abzurufen](mobile-forms-best-practices.md).

## Siehe auch {#see-also}

* [Überblick](overview.md)
* [Architektur](architecture.md)
* [Häufig gestellte Fragen](faq.md)
* [Erstellen und Veröffentlichen eines Headless-Formulars](create-and-publish-a-headless-form.md)
* [Headless-APIs für adaptive Formulare](https://opensource.adobe.com/aem-forms-af-runtime/api/)
* [Code-Playground](https://experienceleague.adobe.com/landing/aem-headless-forms/developer/code.html?lang=de)
* [Storybook](https://opensource.adobe.com/aem-forms-af-runtime/storybook/)
