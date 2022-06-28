---
title: Cos’è l’API di Adobe Recommendations?
description: Questa esercitazione illustra le pratiche pratiche pratiche degli sviluppatori che utilizzano le API Recommendations di Adobe Target per configurare e gestire i cataloghi Recommendations e i criteri personalizzati, nonché l’utilizzo dell’API di consegna per recuperare il contenuto dei consigli.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 3%

---

# Panoramica API di Adobe Recommendations

API pertinenti per [!DNL Recommendations] include [API amministratore](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) che consentono di:

* Gestire il catalogo di prodotti o contenuti consigliati
* Gestire [!DNL Recommendations] algoritmi e attività

Utilizzo della [!DNL Target] [API di consegna](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) con Recommendations è inoltre possibile:

* Recupera i consigli in oggetti JSON, HTML o XML in modo che possano essere visualizzati su web, dispositivi mobili, e-mail, Internet of Things (IOT) e altri canali.

## Descrizione del tutorial

Questa esercitazione illustra agli sviluppatori le pratiche pratiche pratiche che utilizzano [!DNL Recommendations] API da configurare e gestire [!DNL Recommendations] cataloghi e criteri personalizzati, nonché utilizzo dell’API di consegna per recuperare il contenuto dei consigli. Al termine dell’esercitazione, potrai:

* Configurare e gestire le entità tramite l’API di Recommendations
* Configurare e gestire criteri personalizzati tramite l’API di Recommendations
* Scopri come utilizzare Recommendations con l’API di consegna per utilizzare i risultati dei consigli su dispositivi non HTML

## Destinatari

Questa esercitazione è destinata agli sviluppatori che non hanno mai utilizzato le API di Target o Recommendations.

## Prerequisiti

L&#39;utilizzo delle API di amministrazione di Target richiede [Impostazione di autenticazione Adobe](https://developer.adobe.com/target/before-administer/configure-authentication/){target=_blank}. Assicurati di aver configurato questo prima di iniziare questa esercitazione.

## Risorse

Tieni presente le risorse seguenti, necessarie per comprendere questa esercitazione e seguirla con successo:

| Risorsa | Dettagli |
| --- | --- |
| Postman | Ottieni il [app Postman](https://www.postman.com/downloads/) per il sistema operativo in uso. Postman basic è gratuita con la creazione dell’account. Sebbene non sia necessario per utilizzare le API di Adobe Target in generale, Postman semplifica i flussi di lavoro API e Adobe Target fornisce diverse raccolte Postman per aiutarti a eseguire le API e imparare come funzionano. Il resto di questa esercitazione presuppone il funzionamento di Postman. Per assistenza, fare riferimento al [Documentazione di Postman](https://learning.getpostman.com/). |
| Riferimenti | Nel resto dell’esercitazione viene utilizzata la familiarità con le seguenti risorse:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentazione di Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentazione API di Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Avanti &quot;Gestisci il tuo catalogo Recommendations&quot; >](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=_blank}
