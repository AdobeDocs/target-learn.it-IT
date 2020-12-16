---
title: Implementare i provider di dati per integrare dati di terze parti in  Adobe Target
seo-title: Implementare i provider di dati per integrare dati di terze parti in  Adobe Target
description: Dettagli di implementazione ed esempi di utilizzo  funzione Fornitori dati Adobe Target per recuperare dati da fornitori di dati di terze parti e trasmetterli nella richiesta Target.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Implementazione di [!UICONTROL provider di dati] per integrare dati di terze parti in  Adobe Target

Dettagli di implementazione ed esempi su come utilizzare  funzione Adobe Target [!UICONTROL Data Providers] per recuperare i dati dai provider di dati di terze parti e trasmetterli nella richiesta Target.

>[!NOTE]
>
>[!UICONTROL I ] provider di dati richiedono  `at.js` 1.3 o versione successiva

## Implementazione dei componenti di base dei provider di dati

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Panoramica rapida dei componenti di base di un `dataProvider` e di come ottenere il codice nell&#39;ordine corretto.\
Un esempio di lavoro con il codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrazione con un&#39;API di terze parti

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Un esempio più realistico, l&#39;integrazione di un&#39;API meteorologica.\
Un esempio di lavoro con il codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrazione con provider multipli

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Come incorporare dati da più provider nella richiesta globale [!DNL Target].\
Un esempio di lavoro con il codice utilizzato nel video è disponibile qui:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Riduci impatto sul caricamento della pagina

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Riducete al minimo l&#39;impatto sul tempo di caricamento della pagina memorizzando i dati in un oggetto di memorizzazione della sessione. In alternativa, è possibile trasmettere i valori come parametri di profilo utilizzando il prefisso `profile.`, e trasmetterli nella prima [!DNL Target] richiesta della sessione. Tuttavia, potete trasmettere solo cinquanta parametri di profilo per richiesta.

Un esempio di lavoro con il codice utilizzato nel video è disponibile qui: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiali di supporto

* [Utilizzare i provider di dati con  Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Documentazione sui provider di dati](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)