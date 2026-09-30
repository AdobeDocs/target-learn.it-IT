---
title: Cos’è l’API di Adobe Recommendations?
description: Questo tutorial illustra agli sviluppatori le procedure pratiche per l’utilizzo delle API di Adobe Target Recommendations per configurare e gestire cataloghi e criteri personalizzati di Recommendations, nonché per l’utilizzo delle API di consegna per recuperare i contenuti di Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
TQID: 'https://experienceleague.adobe.com/NQpsNnhLA0MRP-pJQLS35ymJ2lnulZebvI-Yv4-xSxw'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
    internal-label: Administration and configuration
  - id: f69bc5f1-ebdb-4306-a281-f2e77daf734c
    internal-label: Activities and tests
subfeature_v2:
  - id: ed58f4a1-16eb-4c8c-b505-be9da766a9ec
    internal-label: Recommendations
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
    internal-label: Overview
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: d11449f8685d14c2bbd1e70f80711d4edab9d3a1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 6%
---
# Panoramica API di Adobe Recommendations

Le API rilevanti per [!DNL Recommendations] includono [API amministratore](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=it) che consentono di:

* Gestione del catalogo di prodotti o contenuti consigliati
* Gestisci gli algoritmi e le attività di [!DNL Recommendations]

Utilizzando l&#39;[!DNL Target] [API di consegna](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=it) con Recommendations, puoi anche:

* Recupera i consigli in oggetti JSON, HTML o XML in modo che possano essere visualizzati in web, dispositivi mobili, e-mail, Internet of Things (IOT) e altri canali.

## Descrizione del tutorial

Questo tutorial illustra agli sviluppatori le procedure pratiche per l&#39;utilizzo delle API [!DNL Recommendations] per configurare e gestire cataloghi [!DNL Recommendations] e criteri personalizzati, nonché per l&#39;utilizzo dell&#39;API di consegna per recuperare il contenuto dei consigli. Al termine di questa esercitazione, sarai in grado di:

* Configurare e gestire le entità tramite l’API Recommendations
* Configurare e gestire criteri personalizzati utilizzando l’API di Recommendations
* Scopri come utilizzare Recommendations con l’API di consegna per utilizzare i risultati dei consigli in dispositivi non HTML

## Pubblico

Questo tutorial è destinato agli sviluppatori che utilizzano per la prima volta le API di Target o le API di Recommendations.

## Prerequisiti

L&#39;utilizzo delle API dell&#39;amministratore di Target richiede [l&#39;impostazione dell&#39;autenticazione di Adobe](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html?lang=it){target="_blank"}. Assicurati di averlo configurato prima di iniziare questa esercitazione.

## Risorse

Prendi nota delle seguenti risorse, necessarie per comprendere questa esercitazione e seguirla correttamente:

| Risorsa | Dettagli |
| --- | --- |
| Postman | Scarica l&#39;[app Postman](https://www.postman.com/downloads/) per il tuo sistema operativo. Postman basic è gratuito con la creazione dell&#39;account. Anche se non è necessario per utilizzare le API di Adobe Target in generale, Postman semplifica i flussi di lavoro API e Adobe Target fornisce diverse raccolte Postman per aiutarle a eseguire le API e a imparare a utilizzarle. Il resto di questo tutorial presuppone una conoscenza operativa di Postman. Per assistenza, fare riferimento alla [documentazione di Postman](https://learning.getpostman.com/). |
| Riferimenti | Per il resto di questa esercitazione si presume che le risorse seguenti siano familiari:<UL><li>[Github Adobe I/O](https://github.com/adobeio)</li><li>[Documentazione di Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentazione API per la funzione Consigli](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Avanti &quot;Gestire il catalogo dei consigli&quot; >](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html?lang=it){target="_blank"}
