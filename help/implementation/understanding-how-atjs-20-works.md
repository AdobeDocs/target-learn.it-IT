---
title: Come funziona at.js 2.0?
description: Scopri in che modo at.js 2.0 migliora il supporto di Adobe Target per le applicazioni a pagina singola (SPA) e si integra con altre soluzioni Experience Cloud.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
TQID: https://experienceleague.adobe.com/yi78hasak-rtlhpCG4-UnewWXAwMfPZJSpw9sFzRenU
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 396
ht-degree: 0%

---

# Come funziona at.js 2.0 di Adobe Target

`at.js` 2.0 migliora il supporto di Adobe Target per le applicazioni a pagina singola (SPA) e si integra con altre soluzioni Experience Cloud. Questo video e i relativi diagrammi spiegano come tutto si combina.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagrammi architettura

Comportamento di ![at.js 2.0 al caricamento della pagina](assets/pageload.png)

1. La chiamata restituisce Experience Cloud ID (ECID). Se l&#39;utente è autenticato, un&#39;altra chiamata sincronizza l&#39;ID cliente.

1. La libreria `at.js` viene caricata in modo sincrono e nasconde il corpo del documento (`at.js` può anche essere caricato in modo asincrono con un frammento pre-hiding opzionale implementato nella pagina).

1. Viene effettuata una richiesta di caricamento della pagina, con tutti i parametri configurati, ECID, SDID e ID cliente.

1. Gli script di profilo vengono eseguiti e inseriti in [!UICONTROL Profile Store]. L&#39;archivio richiede tipi di pubblico idonei da [!UICONTROL Audience Library] (ad esempio pubblici condivisi da [!DNL Analytics], Audience Manager, ecc.). [!UICONTROL Customer Attributes] sono inviati a [!UICONTROL Profile Store] in un processo batch.
1. In base all&#39;URL, ai parametri di richiesta e ai dati di profilo, [!DNL Target] decide quali attività ed esperienze restituire al visitatore per la pagina corrente e le viste future

1. Contenuto di destinazione rinviato alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione.

   Il contenuto mirato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.

   Il contenuto mirato per le viste future di un’applicazione a pagina singola viene memorizzato nella cache del browser, in modo da applicarlo immediatamente senza una chiamata al server aggiuntiva quando si attivano le viste. (vedere il diagramma successivo per il comportamento `triggerView()`).

1. [!DNL Analytics] dati inviati dalla pagina ai server [!UICONTROL Data Collection]
1. I dati di [!DNL Target] vengono confrontati con i dati di Analytics tramite SDID ed elaborati nell&#39;archivio dei report di [!DNL Analytics]. I dati di [!DNL Analytics] possono quindi essere visualizzati sia in [!DNL Analytics] che in [!DNL Target] tramite i rapporti A4T.

Comportamento di ![at.js 2.0 quando si utilizza la funzione triggerView()](assets/triggerview.png)

1. Chiamata di `adobe.target.triggerView()` nell&#39;applicazione a pagina singola
1. Il contenuto di destinazione per la visualizzazione viene letto dalla cache

1. Il contenuto di destinazione viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito

1. Richiesta di notifica inviata a [!DNL Target] [!UICONTROL Profile Store] per conteggiare il visitatore nell&#39;attività e nelle metriche incrementali
1. [!DNL Analytics] dati inviati dall&#39;applicazione a pagina singola ai server [!UICONTROL Data Collection]

1. I dati di [!DNL Target] vengono inviati dal backend [!DNL Target] ai server [!UICONTROL Data Collection]. I dati di [!DNL Target] corrispondono ai dati di [!DNL Analytics] tramite SDID ed vengono elaborati nell&#39;archivio dei report di [!DNL Analytics]. I dati di [!DNL Analytics] possono quindi essere visualizzati sia in [!DNL Analytics] che in [!DNL Target] tramite i rapporti A4T.

## Risorse aggiuntive

* [Implementare at.js 2.0 in un’applicazione a pagina singola](implement-atjs-20-in-a-single-page-application.md)
* [Utilizzare il Compositore esperienza visivo di Adobe Target per applicazioni a pagina singola](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
