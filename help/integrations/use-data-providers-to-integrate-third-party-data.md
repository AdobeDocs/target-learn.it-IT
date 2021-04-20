---
title: Come utilizzare i provider di dati per integrare dati di terze parti
description: Questa esercitazione introduce gli utenti ai provider di dati. Scopri come utilizzare la funzionalità Fornitori di dati per trasferire facilmente dati da terze parti ad Adobe Target.
role: Business Practitioner, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 22%

---


# Utilizza Fornitori di dati per integrare dati di terze parti in Adobe Target

[!UICONTROL Fornitori di dati è una funzionalità che ti permette di trasmettere facilmente dati da terze parti a Target.  ]  Un esempio di terza parte potrebbe essere un servizio meteo, un DMP o persino il tuo servizio web. Puoi utilizzare questi dati per generare tipi di pubblico e contenuti mirati e per arricchire il profilo del visitatore.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Come utilizzare Fornitori di dati

1. L’esperto di implementazione aggiunge il codice prima di at.js (o nella sezione Intestazione libreria di at.js) che effettua la chiamata API a terze parti, analizza la risposta e specifica con coppie nome/valore dalla risposta da inviare a [!DNL Target].
1. at.js gestisce la visualizzazione momentanea di altri contenuti e include le coppie nome/valore come parametri personalizzati nella richiesta globale di Target.
1. L’addetto al marketing crea i tipi di pubblico nell’interfaccia [!DNL Target] in base a questi parametri personalizzati.
1. L’addetto al marketing utilizza questi tipi di pubblico per eseguire il targeting di esperienze, attività e metriche, nonché per i tipi di pubblico per reportistica.

>[!NOTE]
>
>[!UICONTROL Fornitori di dati ] richiede at.js 1.3 o versione successiva

## Materiali di supporto

* [Implementazione di Fornitori di dati in at.js e Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
* [Documentazione Fornitori di dati](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)