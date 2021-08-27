---
title: Cos’è l’API di Adobe Recommendations?
description: Questa esercitazione illustra le pratiche pratiche pratiche degli sviluppatori che utilizzano le API Recommendations di Adobe Target per configurare e gestire i cataloghi Recommendations e i criteri personalizzati, nonché l’utilizzo dell’API di consegna per recuperare il contenuto dei consigli.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%

---

# Panoramica API di Adobe Recommendations

Le API rilevanti per [!DNL Recommendations] includono [API amministratore](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) che consentono di:

* Gestire il catalogo di prodotti o contenuti consigliati
* Gestire gli algoritmi e le attività [!DNL Recommendations]

Utilizzando [!DNL Target] [API di consegna](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) con Recommendations, puoi anche:

* Recupera i consigli in oggetti JSON, HTML o XML in modo che possano essere visualizzati su web, dispositivi mobili, e-mail, Internet of Things (IOT) e altri canali.

## Descrizione del tutorial

Questa esercitazione illustra agli sviluppatori le pratiche pratiche pratiche che utilizzano le API [!DNL Recommendations] per configurare e gestire i cataloghi e i criteri personalizzati [!DNL Recommendations], nonché l’utilizzo dell’API di consegna per recuperare il contenuto dei consigli. Al termine dell’esercitazione, potrai:

* Configurare e gestire le entità tramite l’API di Recommendations
* Configurare e gestire criteri personalizzati tramite l’API di Recommendations
* Scopri come utilizzare Recommendations con l’API di consegna per utilizzare i risultati dei consigli nei dispositivi non HTML

## Destinatari

Questa esercitazione è destinata agli sviluppatori che non hanno mai utilizzato le API di Target o Recommendations.

## Prerequisiti

L&#39;utilizzo delle API di amministrazione di Target richiede [configurazione dell&#39;autenticazione Adobe](../apis/configure-io-target-integration.md). Assicurati di aver configurato questo prima di iniziare questa esercitazione.

## Risorse

Tieni presente le risorse seguenti, necessarie per comprendere questa esercitazione e seguirla con successo:

| Risorsa | Dettagli |
| --- | --- |
| Postman | Scarica l’ [App Postman](https://www.postman.com/downloads/) per il tuo sistema operativo. Postman Basic è gratuito con la creazione dell&#39;account. Anche se non è necessario per utilizzare le API di Adobe Target in generale, Postman semplifica i flussi di lavoro API e Adobe Target fornisce diverse raccolte Postman per aiutarti a eseguire le API e imparare come funzionano. Il resto di questo tutorial presuppone la conoscenza di lavoro di Postman. Per assistenza, fai riferimento alla [documentazione Postman](https://learning.getpostman.com/). |
| Riferimenti | Nel resto dell’esercitazione viene utilizzata la familiarità con le seguenti risorse:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentazione di Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentazione API di Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Avanti &quot;Gestisci il tuo catalogo Recommendations&quot; >](manage-catalog.md)
