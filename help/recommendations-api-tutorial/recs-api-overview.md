---
title: ' API di Adobe Recommendations'
keywords: recommendations;adobe recommendations;premium;api;apis
description: ' Adobe Target Recommendations include un set dedicato di API che consentono di gestire il catalogo di prodotti e/o contenuti raccomandabili; gestire gli algoritmi e le campagne di raccomandazione; e distribuite raccomandazioni in oggetti JSON, HTML o XML da visualizzare in Web, dispositivi mobili, e-mail, IOT e altri canali.'
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---


#  API di Adobe Recommendations

Le API rilevanti per [!DNL Recommendations] includono [API admin](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) che consentono di:

* Gestione del catalogo di prodotti o contenuti raccomandabili
* Gestione degli algoritmi e delle attività [!DNL Recommendations]

Utilizzando l&#39;API [!DNL Target] [di consegna](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) con Recommendations, potete anche:

* Recuperate le raccomandazioni negli oggetti JSON, HTML o XML in modo che possano essere visualizzate in Web, dispositivi mobili, e-mail, Internet of Things (IOT) e altri canali.

## Descrizione dell&#39;esercitazione

Questa esercitazione guida gli sviluppatori attraverso pratiche pratiche pratiche utilizzando le [!DNL Recommendations] API per configurare e gestire [!DNL Recommendations] cataloghi e criteri personalizzati, nonché utilizzando l&#39;API di consegna per recuperare il contenuto delle raccomandazioni. Al termine di questa esercitazione, potrete:

* Configurare e gestire le entità tramite l&#39;API Recommendations
* Configurare e gestire criteri personalizzati tramite l&#39;API Recommendations
* Comprendere come utilizzare Recommendations con l&#39;API di distribuzione per utilizzare i risultati delle raccomandazioni su dispositivi non HTML

## Destinatari

Questa esercitazione è destinata agli sviluppatori che non hanno mai utilizzato API Target o API Recommendations.

## Prerequisiti

L&#39;utilizzo delle API di amministrazione di Target richiede [ configurazione dell&#39;autenticazione del Adobe](../apis/configure-io-target-integration.md). Accertatevi che sia configurato prima di iniziare l&#39;esercitazione.

## Risorse

Tenete presenti le risorse seguenti, necessarie per comprendere meglio questa esercitazione e per seguirla correttamente:

| Risorsa | Dettagli |
| --- | --- |
| Postman | Scaricate l&#39;app [Postman](https://www.postman.com/downloads/) per il sistema operativo in uso. Postman Basic è gratuito con la creazione di account. Sebbene non sia richiesto per utilizzare  API Adobe Target in generale, Postman semplifica i flussi di lavoro API e  Adobe Target fornisce diverse raccolte Postman per aiutare a eseguire le sue API e imparare come funzionano. Il resto di questa esercitazione presuppone una conoscenza attiva di Postman. Per assistenza, fare riferimento alla [documentazione Postman](https://learning.getpostman.com/). |
| Riferimenti | Nel resto dell&#39;esercitazione viene utilizzata la familiarità con le seguenti risorse:<UL><li>[ Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentazione su Target  Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentazione API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Avanti &quot;Gestisci il tuo Recommendations Catalog&quot; >](manage-catalog.md)
