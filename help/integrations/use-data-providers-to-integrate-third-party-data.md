---
title: Utilizzare i provider di dati per integrare dati di terze parti
description: Questa esercitazione presenta gli utenti ai provider di dati. Scopri come utilizzare la funzionalità Fornitori di dati per passare facilmente i dati da terze parti ad Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 25%

---

# Utilizza Data Provider per integrare dati di terze parti in Adobe Target

[!UICONTROL Fornitori di dati è una funzionalità che ti permette di trasmettere facilmente dati da terze parti a Target.  ]  Un esempio di terza parte potrebbe essere un servizio meteo, un DMP o persino il tuo servizio web. Puoi utilizzare questi dati per generare tipi di pubblico e contenuti mirati e per arricchire il profilo del visitatore.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Come utilizzare i provider di dati

1. L’esperto dell’implementazione aggiunge codice prima di at.js (o nella sezione Intestazione libreria di at.js) che effettua la chiamata API a terze parti, analizza la risposta e specifica con coppie nome/valore dalla risposta da inviare a [!DNL Target].
1. at.js gestisce la visualizzazione momentanea di altri contenuti e include le coppie nome/valore come parametri personalizzati nella richiesta Target globale.
1. L’addetto al marketing crea tipi di pubblico in [!DNL Target] basata su questi parametri personalizzati.
1. L’addetto al marketing utilizza questi tipi di pubblico per eseguire il targeting di esperienze, attività e metriche, nonché per i tipi di pubblico di reporting.

>[!NOTE]
>
>[!UICONTROL Fornitori di dati] richiede at.js 1.3 o versione successiva

## Materiali di supporto

* [Implementare i provider di dati in at.js e Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
