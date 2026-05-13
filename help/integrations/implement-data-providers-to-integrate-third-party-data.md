---
title: Come implementare i provider di dati per integrare i dati di terze parti
description: Questo tutorial fornisce dettagli sull’implementazione ed esempi sull’utilizzo della funzione Fornitori di dati di Adobe Target per recuperare dati da fornitori di dati terzi e trasmetterli alla richiesta Target.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
TQID: https://experienceleague.adobe.com/Oh0ngUGA-ZfpPHnQnN0VRgUG1ta4yqg8Pfm8mhCZTN0
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 293
ht-degree: 0%

---

# Implementa [!UICONTROL Data Providers] per integrare dati di terze parti in Adobe Target

Dettagli di implementazione ed esempi di come utilizzare la funzione [!UICONTROL Data Providers] di Adobe Target per recuperare dati da provider di dati terzi e trasmetterli nella richiesta Target.

>[!NOTE]
>
>[!UICONTROL Data Providers] richiede `at.js` 1.3 o versione successiva

## Implementare i componenti di base dei provider di dati

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Panoramica rapida dei componenti di base di `dataProvider` e di come ottenere il codice nell&#39;ordine corretto.\
Un esempio di funzionamento del codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrare con un’API di terze parti

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Un esempio più realistico, l’integrazione di un’API meteo.\
Un esempio di funzionamento del codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrare con più provider

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Come incorporare dati provenienti da più provider nella richiesta globale di [!DNL Target].\
Un esempio di funzionamento del codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Riduci al minimo l&#39;impatto del caricamento della pagina

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Riduci al minimo l’impatto sul tempo di caricamento della pagina memorizzando i dati in un oggetto di archiviazione della sessione. In alternativa, è possibile passare i valori come parametri di profilo utilizzando il prefisso `profile.` e semplicemente trasmetterli nella prima richiesta [!DNL Target] della sessione. Tuttavia, ti sarà limitato il passaggio di cinquanta parametri di profilo per richiesta.

Un esempio di funzionamento con il codice utilizzato nel video è disponibile qui: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiali di supporto

* [Utilizzare i provider di dati con Adobe Target](use-data-providers-to-integrate-third-party-data.md)
