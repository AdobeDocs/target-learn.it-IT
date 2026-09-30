---
title: Utilizzare i provider di dati per integrare dati di terze parti
description: Questa esercitazione presenta gli utenti ai provider di dati. Scopri come utilizzare la funzionalità Fornitori di dati per passare facilmente i dati da terze parti ad Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt:
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
TQID: 'https://experienceleague.adobe.com/XiUlJGHSFVxAMqdl6Y7hK9PoXOgiiUI43vrFeAj2Rpo'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: d11449f8685d14c2bbd1e70f80711d4edab9d3a1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 16%
---
# Utilizza Data Provider per integrare dati di terze parti in Adobe Target

[!UICONTROL Fornitori di dati] è una funzionalità che consente di trasmettere facilmente dati da terze parti a Target.  Un esempio di terza parte potrebbe essere un servizio meteo, un DMP o persino il tuo servizio web. Puoi utilizzare questi dati per generare tipi di pubblico e contenuti mirati e per arricchire il profilo del visitatore.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Come utilizzare i provider di dati

1. L&#39;esperto dell&#39;implementazione aggiunge codice prima di at.js (o nella sezione Intestazione libreria di at.js) che effettua la chiamata API alla terza parte, analizza la risposta e specifica coppie nome/valore dalla risposta da inviare a [!DNL Target].
1. at.js gestisce la visualizzazione momentanea di altri contenuti e include le coppie nome/valore come parametri personalizzati nella richiesta Target globale.
1. L&#39;addetto al marketing crea tipi di pubblico nell&#39;interfaccia [!DNL Target] in base a questi parametri personalizzati.
1. L’addetto al marketing utilizza questi tipi di pubblico per eseguire il targeting di esperienze, attività e metriche, nonché per i tipi di pubblico di reporting.

>[!NOTE]
>
>[!UICONTROL Fornitori di dati] richiede at.js 1.3 o versione successiva

## Materiali di supporto

* [Implementare i provider di dati in at.js e Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
