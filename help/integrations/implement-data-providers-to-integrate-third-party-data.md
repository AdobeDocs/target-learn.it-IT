---
title: Come implementare i provider di dati per integrare dati di terze parti
description: Questa esercitazione fornisce dettagli di implementazione ed esempi su come utilizzare la funzione Fornitori di dati di Adobe Target per recuperare dati da fornitori di dati terzi e trasmetterli nella richiesta Target.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Implementa [!UICONTROL Fornitori di dati] per integrare dati di terze parti in Adobe Target

Dettagli di implementazione ed esempi su come utilizzare la funzione Adobe Target [!UICONTROL Fornitori di dati] per recuperare dati da fornitori di dati terzi e trasmetterli nella richiesta Target.

>[!NOTE]
>
>[!UICONTROL Fornitori ] di dati richiede  `at.js` versione 1.3 o successiva

## Implementare i componenti di base dei provider di dati

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Panoramica rapida dei componenti di base di un `dataProvider` e di come ottenere il codice nell’ordine corretto.\
Un esempio di lavoro con il codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrazione con un’API di terze parti

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Un esempio più realistico, l’integrazione di un’API per il meteo.\
Un esempio di lavoro con il codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrazione con più provider

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Come incorporare i dati di più provider nella richiesta globale [!DNL Target].\
Un esempio di lavoro con il codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Riduci a icona l’impatto del caricamento della pagina

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Riduci al minimo l&#39;impatto sul tempo di caricamento della pagina memorizzando i dati in un oggetto di archiviazione sessione. In alternativa, puoi trasmettere i valori come parametri di profilo utilizzando il prefisso `profile.` e solo nella prima [!DNL Target] richiesta della sessione. Tuttavia, potresti essere limitato a passare cinquanta parametri di profilo per richiesta.

Un esempio di lavoro con il codice utilizzato nel video è disponibile qui: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiali di supporto

* [Utilizzare Fornitori di dati con Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Documentazione Fornitori di dati](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)