---
title: Cos’è l’API di Adobe Recommendations?
description: Questo tutorial illustra agli sviluppatori le procedure pratiche per l’utilizzo delle API Recommendations di Adobe Target per configurare e gestire cataloghi Recommendations e criteri personalizzati, nonché per l’utilizzo dell’API di consegna per recuperare i contenuti dei consigli.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: 542ff406fc24df54a2f1b007422492341ea46507
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# Panoramica API di Adobe Recommendations

Le API rilevanti per [!DNL Recommendations] includono [API amministratore](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) che consentono di:

* Gestione del catalogo di prodotti o contenuti consigliati
* Gestisci gli algoritmi e le attività di [!DNL Recommendations]

Utilizzando l&#39;[!DNL Target] [API di consegna](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) con Recommendations, è inoltre possibile:

* Recupera i consigli in oggetti JSON, HTML o XML per visualizzarli in web, dispositivi mobili, e-mail, Internet of Things (IOT) e altri canali.

## Descrizione del tutorial

Questo tutorial illustra agli sviluppatori le procedure pratiche per l&#39;utilizzo delle API [!DNL Recommendations] per configurare e gestire cataloghi [!DNL Recommendations] e criteri personalizzati, nonché per l&#39;utilizzo dell&#39;API di consegna per recuperare il contenuto dei consigli. Al termine di questa esercitazione, sarai in grado di:

* Configurare e gestire le entità tramite l’API Recommendations
* Configurare e gestire criteri personalizzati utilizzando l’API di Recommendations
* Scopri come utilizzare Recommendations con l’API di consegna per utilizzare i risultati dei consigli in dispositivi non HTML.

## Destinatari

Questo tutorial è destinato agli sviluppatori che utilizzano per la prima volta le API di Target o Recommendations.

## Prerequisiti

L&#39;utilizzo delle API dell&#39;amministratore di Target richiede [l&#39;impostazione dell&#39;autenticazione Adobe](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html?lang=it){target="_blank"}. Assicurati di averlo configurato prima di iniziare questa esercitazione.

## Risorse

Prendi nota delle seguenti risorse, necessarie per comprendere questa esercitazione e seguirla correttamente:

| Risorsa | Dettagli |
| --- | --- |
| Postman | Scarica l&#39;[app Postman](https://www.postman.com/downloads/) per il tuo sistema operativo. Postman basic è gratuito con la creazione dell&#39;account. Anche se non è necessario per utilizzare le API di Adobe Target in generale, Postman semplifica i flussi di lavoro API e Adobe Target fornisce diverse raccolte Postman per aiutarle a eseguire le API e a imparare a utilizzarle. Il resto di questo tutorial presuppone una conoscenza operativa di Postman. Per assistenza, fare riferimento alla [documentazione di Postman](https://learning.getpostman.com/). |
| Riferimenti | Per il resto di questa esercitazione si presume che le risorse seguenti siano familiari:<UL><li>[Github Adobe I/O](https://github.com/adobeio)</li><li>[Documentazione Adobe I/O di Target](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentazione API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Avanti &quot;Gestire il catalogo Recommendations&quot; >](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html){target="_blank"}
