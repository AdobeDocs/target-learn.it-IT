---
title: ' API di Adobe Target'
keywords: recommendations;adobe recommendations;premium;api;apis
description: ' Adobe Target Recommendations include un set dedicato di API che consentono di gestire il catalogo di prodotti e/o contenuti raccomandabili; gestire gli algoritmi e le campagne di raccomandazione; e distribuite raccomandazioni in oggetti JSON, HTML o XML da visualizzare in Web, dispositivi mobili, e-mail, IOT e altri canali.'
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b66dbae616c9559f5d1b7bbedf2d9b383840973b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 1%

---


#  API di Adobe Target

 le API Adobe Target possono essere raggruppate in base al tipo.

| Tipo API | Cosa consente di fare | Collegamento di download |
| --- | --- | --- |
| Amministrazione | Creazione, modifica ed eliminazione di attività, audience, offerte e altri oggetti (incluse [!DNL Recommendations] entità, criteri, progettazioni e così via). Le [!DNL Recommendations] API sono un tipo di API admin.) | <UL><li>[Raccolta Postman API di amministrazione di Target](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul> |
| Consegna | Recuperate contenuti ottimizzati e personalizzati da [!DNL Target] distribuire a un utente finale. | [Raccolta Postman API Target Delivery](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection) |
| Generazione di rapporti | Esporta risultati attività e altri risultati di reporting. | Le API di reporting sono incluse nella raccolta [Postman API di amministrazione di](https://developers.adobetarget.com/api/#admin-postman-collection)Target. |
| Profilo | Recuperate e modificate i profili utente memorizzati in  Adobe Target. | [Raccolta Postman API profilo di destinazione](https://developers.adobetarget.com/api/#profiles) |

Notate la distinzione tra le API **** di amministrazione (comprese le [!DNL Recommendations] API), che vi consente di configurare vari aspetti di  Adobe Target, rispetto alle API **di** distribuzione, che consentono di recuperare il contenuto. Le API di amministrazione richiedono l&#39;autenticazione, mentre le API di consegna no.

Per utilizzare  Adobe Target Admin API, è innanzitutto necessario configurare l&#39;autenticazione mediante  I/O Adobe.

[Next &quot;Configure Authentication&quot; (Configura autenticazione) >](configure-io-target-integration.md)
