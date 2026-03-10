---
title: Verwenden benutzerdefinierter Komponenten zum Rendern eines Headless-Formulars
description: Erfahren Sie, wie Sie benutzerdefinierte Komponenten erstellen und sie adaptiven Forms-Headless-Feldern zuordnen. In diesem Handbuch wird erläutert, wie Komponenten nach Feldtyp und Ressourcentyp zugeordnet werden, um benutzerdefiniertes Rendering und Verhalten zu erzielen.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Headless
role: Admin, Developer
level: Beginner, Intermediate
hide: false
exl-id: 5aba1821-35dc-4da4-b188-d4853d64d5ee
source-git-commit: 780f06a39c75dbf8795ac7a971150410ed7981e9
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Verwenden benutzerdefinierter Komponenten zum Rendern eines Headless-Formulars {#developing-for-headless-forms-using-your-own-components}

In Headless Adaptive Forms können Sie benutzerdefinierte Komponenten erstellen und implementieren, um das Erscheinungsbild und die Funktionalität Ihrer Formulare zu definieren. Während die Standardkomponenten Standardverhalten bereitstellen, benötigen Sie möglicherweise bestimmte Benutzeroberflächenelemente oder Interaktionen - wie eine benutzerdefinierte „Ankündigung“-Komponente oder ein spezielles „Freihandsignatur“-Feld.

Dieser Artikel führt Sie durch die Erstellung einer benutzerdefinierten React-Komponente und deren Zuordnung zu Ihrem adaptiven Headless-Formular.

## &#x200B;1. Erstellen einer benutzerdefinierten React-Komponente

Erstellen Sie zunächst die React-Komponente, die das Formularfeld rendert. Diese Komponente kann jede React-Bibliothek verwenden (z. B. Material-Benutzeroberfläche, Ant-Design oder Ihre eigenen benutzerdefinierten Stile).

Erstellen wir beispielsweise eine benutzerdefinierte Komponente **Ankündigung** die eine schreibgeschützte Nachricht mit bestimmtem Stil rendert.

1. Navigieren Sie zum Komponentenverzeichnis Ihres React-Projekts (z. B. `src/components`).
2. Erstellen Sie einen neuen Ordner und eine neue Datei für Ihre Komponente, z. B. `Announcement/index.tsx`.
3. Implementieren Sie die -Komponente. Sie sollte `props` akzeptieren, die mit der Headless-Forms-Laufzeit kompatibel sind (normalerweise den Status des Felds erhalten).

```tsx
import React from 'react';
import { useRuleEngine } from '@aemforms/af-react-renderer';
import { FieldJson, State } from '@aemforms/af-core';

const Announcement = function (props: State<FieldJson>) {
    // The useRuleEngine hook connects the component to the form logic
    const [state, handlers] = useRuleEngine(props);

    if (!state.visible) {
        return null;
    }

    return (
        <div className="custom-announcement" style={{ border: '1px solid #ccc', padding: '10px', backgroundColor: '#f9f9f9' }}>
            <h3>{state?.label?.value}</h3>
            <p>{state?.default}</p>
        </div>
    );
}

export default Announcement;
```

## &#x200B;2. Zuordnen der benutzerdefinierten Komponente

Um Ihre benutzerdefinierte Komponente zu verwenden, müssen Sie sie in der `mappings.ts`-Datei zuordnen. Die Headless-Forms-Laufzeit verwendet diese Zuordnung, um zu bestimmen, welche React-Komponente für jedes Feld in der Formular-JSON gerendert werden soll.

Es gibt zwei Möglichkeiten, Komponenten zuzuordnen: nach **Feldtyp** oder nach **Ressourcentyp**.

### Zuordnung nach Feldtyp

Die standardmäßige Zuordnung basiert auf der `fieldType`-Eigenschaft in der Formular-JSON (z. B. `text-input`, `checkbox`, `button`). Dies ist nützlich, wenn Sie (*) Instanzen* Standardkomponente durch Ihre benutzerdefinierte Version ersetzen möchten.

1. Öffnen Sie `src/utils/mappings.ts` (oder wo auch immer Ihre Zuordnungen definiert sind).
2. Importieren Sie Ihre benutzerdefinierte Komponente.
3. Fügen Sie sie dem Zuordnungsobjekt hinzu, indem Sie die `fieldType` als Schlüssel verwenden.

```typescript
import { mappings } from "@aemforms/af-react-components";
import Announcement from "../components/Announcement";

const customMappings: any = {
  ...mappings,
  "text-input": Announcement // This would replace ALL text-input fields (use with caution)
};

export default customMappings;
```

### Zuordnung nach Ressourcentyp (benutzerdefinierte Komponenten)

Wenn Sie eine benutzerdefinierte Komponente in AEM erstellt haben (z. B. eine „Ankündigung“-Komponente, die eine standardmäßige Textkomponente erweitert) und *nur“ diese Komponente* in Ihrer React-App anders rendern möchten, sollten Sie sie nach ihrem **Ressourcentyp** oder einer eindeutigen Kennung zuordnen.

Mit diesem Ansatz können Sie standardmäßige Textkomponenten normal rendern lassen, während Ihre benutzerdefinierte Komponente „Ankündigung“ Ihre spezialisierte React-Implementierung verwendet.

1. Identifizieren Sie die eindeutige Kennung Ihrer Komponente. Im JSON-Formular für Headless ist dies oft in der `:type`-Eigenschaft oder einem benutzerdefinierten `fieldType` zu finden, falls konfiguriert.
2. Fügen Sie die Zuordnung mit dieser Kennung hinzu.

```typescript
import { mappings } from "@aemforms/af-react-components";
import Announcement from "../components/Announcement";

const customMappings: any = {
  ...mappings,
  // Map by resource type or custom identifier
  "my-project/components/announcement": Announcement
};

export default customMappings;
```

> **Hinweis:** Stellen Sie sicher, dass Ihr AEM-Formularmodell die richtige `:type` oder Kennung exportiert, die dem in `mappings.ts` verwendeten Schlüssel entspricht.

## &#x200B;3. Anwenden der Zuordnungen

Stellen Sie abschließend sicher, dass Ihre Headless-Formularinstanz diese benutzerdefinierten Zuordnungen verwendet.

```tsx
import React from 'react';
import { AdaptiveForm } from '@aemforms/af-react-renderer';
import customMappings from './utils/mappings';
import formJSON from './form-def.json';

function App() {
  return (
    <AdaptiveForm
      formJson={formJSON}
      mappings={customMappings}
    />
  );
}

export default App;
```

Wenn Sie diese Schritte ausführen, können Sie die Funktionen Ihres Headless Adaptive Forms mit Komponenten erweitern, die zu Ihrem spezifischen Design und Ihren funktionalen Anforderungen passen.
