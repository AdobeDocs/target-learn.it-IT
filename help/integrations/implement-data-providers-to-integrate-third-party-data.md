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
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Implementare [!UICONTROL Fornitori di dati] integrare dati di terze parti in Adobe Target

Dettagli di implementazione ed esempi di come utilizzare Adobe Target [!UICONTROL Fornitori di dati] per recuperare dati da fornitori di dati terzi e trasmetterli nella richiesta Target.

>[!NOTE]
>
>[!UICONTROL Fornitori di dati] richiede `at.js` 1.3 o superiore

## Implementare i componenti di base dei provider di dati

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Panoramica rapida dei componenti di base di una `dataProvider` e come ottenere il codice nell&#39;ordine giusto.\
Un esempio di funzionamento del codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrare con un’API di terze parti

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Un esempio più realistico, l’integrazione di un’API meteo.\
Un esempio di funzionamento del codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrare con più provider

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Come incorporare dati provenienti da più provider nel tuo [!DNL Target] richiesta.\
Un esempio di funzionamento del codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Riduci al minimo l&#39;impatto del caricamento della pagina

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Riduci al minimo l’impatto sul tempo di caricamento della pagina memorizzando i dati in un oggetto di archiviazione della sessione. In alternativa, è possibile trasmettere i valori come parametri di profilo utilizzando `profile.` e passale nel primo [!DNL Target] richiesta della sessione. Tuttavia, ti sarà limitato il passaggio di cinquanta parametri di profilo per richiesta.

Un esempio di funzionamento del codice utilizzato nel video è disponibile qui: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiali di supporto

* [Utilizzare i provider di dati con Adobe Target](use-data-providers-to-integrate-third-party-data.md)
