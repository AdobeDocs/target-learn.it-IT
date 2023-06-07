---
title: Come funziona at.js 2.0?
description: at.js 2.0 migliora il supporto di Adobe Target per le applicazioni a pagina singola (SPA) e si integra con altre soluzioni Experience Cloud. Questo video e i relativi diagrammi spiegano come tutto si combina.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 22%

---

# Come funziona at.js 2.0 di Adobe Target

`at.js` 2.0 migliora il supporto di Adobe Target per le applicazioni a pagina singola (SPA) e si integra con altre soluzioni Experience Cloud. Questo video e i relativi diagrammi spiegano come tutto si combina.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagrammi architettura

![Comportamento di at.js 2.0 al caricamento della pagina](assets/pageload.png)

1. La chiamata restituisce l’ID Experience Cloud (ECID). Se l&#39;utente è autenticato, un&#39;altra chiamata sincronizza l&#39;ID cliente.

1. `at.js` la libreria viene caricata in modo sincrono e nasconde il corpo del documento (`at.js` può anche essere caricato in modo asincrono con un frammento pre-hiding opzionale implementato sulla pagina).

1. Viene effettuata una richiesta di caricamento della pagina, con tutti i parametri configurati, ECID, SDID e ID cliente.

1. Gli script di profilo vengono eseguiti e inseriti in [!UICONTROL Archivio profili]. L’archivio richiede tipi di pubblico idonei da [!UICONTROL Libreria tipi di pubblico] (ad esempio, tipi di pubblico condivisi da [!DNL Analytics], Audience Manager, ecc.). [!UICONTROL Attributi del cliente] vengono inviati a [!UICONTROL Archivio profili] in un processo batch.
1. In base all’URL, ai parametri di richiesta e ai dati di profilo, [!DNL Target] decide quali attività ed esperienze restituire al visitatore per la pagina corrente e le viste future

1. Contenuto di destinazione rinviato alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione.

   Il contenuto mirato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.

   Il contenuto mirato per le viste future di un’applicazione a pagina singola viene memorizzato nella cache del browser, in modo da applicarlo immediatamente senza una chiamata al server aggiuntiva quando si attivano le viste. (vedere il diagramma seguente per `triggerView()` comportamento).

1. [!DNL Analytics] dati inviati dalla pagina a [!UICONTROL Raccolta dati] Server
1. [!DNL Target]I dati di vengono confrontati con i dati di tramite SDID e vengono elaborati nell’archivio dei rapporti di Analytics. [!DNL Analytics] [!DNL Analytics] I dati possono quindi essere visualizzati in entrambi [!DNL Analytics] e [!DNL Target] tramite i rapporti A4T.

![Comportamento di at.js 2.0 quando si utilizza la funzione triggerView()](assets/triggerview.png)

1. `adobe.target.triggerView()` viene chiamato nell&#39;applicazione a pagina singola
1. Il contenuto mirato per la visualizzazione viene letto dalla cache

1. Il contenuto mirato viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito

1. Si invia la richiesta di notifica all&#39;archivio profili di [!DNL Target] per conteggiare il visitatore nell&#39;attività e nelle metriche incrementali
1. [!DNL Analytics] i dati sono inviati dal SPA al [!UICONTROL Raccolta dati] Server

1. [!DNL Target] i dati vengono inviati da [!DNL Target] back-end per [!UICONTROL Raccolta dati] Server. I dati di [!DNL Target] vengono confrontati con i dati di [!DNL Analytics] tramite SDID e vengono elaborati nell’archivio dei rapporti di [!DNL Analytics]. [!DNL Analytics] I dati possono quindi essere visualizzati in entrambi [!DNL Analytics] e [!DNL Target] tramite i rapporti A4T.

## Risorse aggiuntive

* [Implementare at.js 2.0 in un’applicazione a pagina singola](implement-atjs-20-in-a-single-page-application.md)
* [Utilizzare il Compositore esperienza visivo di Adobe Target per applicazioni a pagina singola (VEC SPA)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
