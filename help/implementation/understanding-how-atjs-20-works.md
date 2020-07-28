---
title: Come funziona  Adobe Target  at.js 2.0
seo-title: Come funziona  Adobe Target  at.js 2.0
description: at.js 2.0 migliora  supporto  Adobe Target per applicazioni a pagina singola (SPA) e si integra con altre soluzioni  Experience Cloud. Questo video e i diagrammi che lo accompagnano spiegano come tutto si combina.
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 20%

---


# Come funziona  Adobe Target  at.js 2.0

`at.js` 2.0 migliora  supporto  Adobe Target per applicazioni a pagina singola (SPA) e si integra con altre soluzioni  Experience Cloud. Questo video e i diagrammi che lo accompagnano spiegano come tutto si combina.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagrammi di architettura

![comportamento at.js 2.0 sul caricamento della pagina](assets/pageload.png)

1. La chiamata restituisce  ID Experience Cloud (ECID). Se l’utente è autenticato, un’altra chiamata sincronizza l’ID cliente.

1. `at.js` la libreria viene caricata in modo sincrono e nasconde il corpo del documento (`at.js` può anche essere caricato in modo asincrono con un frammento di preimpostazione opzionale implementato sulla pagina).

1. La richiesta di caricamento della pagina viene effettuata includendo tutti i parametri configurati, ECID, SDID e ID cliente.

1. Profile scripts execute and feed into the [!UICONTROL Profile Store]. The Store requests qualified audiences from the [!UICONTROL Audience Library] (e.g. audiences shared from [!DNL Analytics], Audience Manager, etc). [!UICONTROL Gli attributi] del cliente vengono inviati a [!UICONTROL Profile Store] in un processo batch.
1. Based on URL, request parameters, and profile data, [!DNL Target] decides which Activities and Experiences to return to the visitor for the current page and future views

1. Contenuto di destinazione inviato di nuovo alla pagina, eventualmente con valori di profilo per un’ulteriore personalizzazione.

   Il contenuto mirato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.

   Il contenuto di destinazione per le visualizzazioni future di un&#39;applicazione a pagina singola viene memorizzato nella cache del browser, in modo che possa essere applicato istantaneamente senza una chiamata server aggiuntiva quando le viste vengono attivate. (Vedere il diagramma seguente per il `triggerView()` comportamento).

1. [!DNL Analytics] i dati inviati dalla pagina ai server di raccolta  dati
1. [!DNL Target]I dati di vengono confrontati con i dati di tramite SDID e vengono elaborati nell’archivio dei rapporti di Analytics. [!DNL Analytics] [!DNL Analytics] i dati possono quindi essere visualizzati sia nei rapporti A4T [!DNL Analytics] che [!DNL Target] tramite.

![comportamento at.js 2.0 quando si utilizza la funzione triggerView()](assets/triggerview.png)

1. `adobe.target.triggerView()` viene chiamato nell’applicazione a pagina singola
1. Il contenuto mirato per la visualizzazione viene letto dalla cache

1. Il contenuto mirato viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito

1. Si invia la richiesta di notifica all&#39;archivio profili di [!DNL Target] per conteggiare il visitatore nell&#39;attività e nelle metriche incrementali
1. [!DNL Analytics] i dati vengono inviati dall&#39;SPA ai server di raccolta  dati

1. [!DNL Target] i dati vengono inviati dal [!DNL Target] back-end ai server di raccolta  dati. I dati di [!DNL Target] vengono confrontati con i dati di [!DNL Analytics] tramite SDID e vengono elaborati nell’archivio dei rapporti di [!DNL Analytics]. [!DNL Analytics] i dati possono quindi essere visualizzati sia nei rapporti A4T [!DNL Analytics] che [!DNL Target] tramite.

## Risorse aggiuntive

* [Implementazione di at.js 2.0 in un&#39;applicazione a pagina singola](implement-atjs-20-in-a-single-page-application.md)
* [Usare  Adobe Target  Visual Experience Composer (Compositore esperienza visivo) per applicazioni a pagina singola (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Come funziona at.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)