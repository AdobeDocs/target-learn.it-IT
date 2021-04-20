---
title: Come funziona at.js 2.0?
description: at.js 2.0 migliora il supporto Adobe Target per le applicazioni a pagina singola (SPA) e si integra con altre soluzioni di Experience Cloud. Questo video e i diagrammi che lo accompagnano spiegano come tutto si unisce.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 21%

---


# Come funziona Adobe Target at.js 2.0

`at.js` La versione 2.0 migliora il supporto Adobe Target per le applicazioni a pagina singola (SPA) e si integra con altre soluzioni Experience Cloud. Questo video e i diagrammi che lo accompagnano spiegano come tutto si unisce.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagrammi di architettura

![Comportamento di at.js 2.0 al caricamento della pagina](assets/pageload.png)

1. La chiamata restituisce Experience Cloud ID (ECID). Se l’utente è autenticato, un’altra chiamata sincronizza l’ID cliente.

1. `at.js` la libreria viene caricata in modo sincrono e nasconde il corpo del documento (`at.js` può anche essere caricato in modo asincrono con un frammento pre-hiding facoltativo implementato nella pagina).

1. Viene effettuata la richiesta di caricamento pagina, con tutti i parametri configurati, ECID, SDID e ID cliente.

1. Gli script di profilo vengono eseguiti e inseriti nell&#39; [!UICONTROL archivio profili]. L&#39;archivio richiede tipi di pubblico qualificati dalla [!UICONTROL Libreria tipi di pubblico] (ad esempio, tipi di pubblico condivisi da [!DNL Analytics], Audience Manager, ecc.). [!UICONTROL Gli ] attributi del cliente vengono inviati a  [!UICONTROL Profile ] Store in un processo batch.
1. In base all’URL, ai parametri di richiesta e ai dati di profilo, [!DNL Target] decide quali attività ed esperienze restituire al visitatore per la pagina corrente e le visualizzazioni future

1. Contenuto di destinazione inviato nuovamente alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione.

   Il contenuto mirato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.

   Il contenuto mirato per le visualizzazioni future di un’applicazione a pagina singola viene memorizzato nella cache del browser, in modo che possa essere applicato immediatamente senza una chiamata al server aggiuntiva quando vengono attivate le visualizzazioni. (Vedi il diagramma seguente per il comportamento `triggerView()` ).

1. [!DNL Analytics] dati inviati dalla pagina ai  [!UICONTROL Data ] CollectionServers
1. [!DNL Target]I dati di vengono confrontati con i dati di tramite SDID e vengono elaborati nell’archivio dei rapporti di Analytics. [!DNL Analytics] [!DNL Analytics] i dati possono quindi essere visualizzati sia nei rapporti  [!DNL Analytics] che  [!DNL Target] tramite A4T.

![Comportamento di at.js 2.0 quando si utilizza la funzione triggerView()](assets/triggerview.png)

1. `adobe.target.triggerView()` viene chiamato nell&#39;applicazione a pagina singola
1. Il contenuto mirato per la visualizzazione viene letto dalla cache

1. Il contenuto mirato viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito

1. Si invia la richiesta di notifica all&#39;archivio profili di [!DNL Target] per conteggiare il visitatore nell&#39;attività e nelle metriche incrementali
1. [!DNL Analytics] i dati vengono inviati dal SPA ai  [!UICONTROL Data ] CollectionServers

1. [!DNL Target] i dati vengono inviati dal  [!DNL Target] backend ai  [!UICONTROL Data ] CollectionServers. I dati di [!DNL Target] vengono confrontati con i dati di [!DNL Analytics] tramite SDID e vengono elaborati nell’archivio dei rapporti di [!DNL Analytics]. [!DNL Analytics] i dati possono quindi essere visualizzati sia nei rapporti  [!DNL Analytics] che  [!DNL Target] tramite A4T.

## Risorse aggiuntive

* [Implementare at.js 2.0 in un’applicazione a pagina singola](implement-atjs-20-in-a-single-page-application.md)
* [Utilizzare il Compositore esperienza visivo di Adobe Target per le applicazioni a pagina singola (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Documentazione sul funzionamento di at.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)