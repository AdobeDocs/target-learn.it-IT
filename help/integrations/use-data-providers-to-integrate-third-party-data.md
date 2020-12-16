---
title: Utilizzare i provider di dati per integrare dati di terze parti in  Adobe Target
seo-title: Utilizzare i provider di dati per integrare dati di terze parti in  Adobe Target
description: Fornitori di dati è una funzionalità che ti permette di trasmettere facilmente dati da terze parti a Target.  Un esempio di terza parte potrebbe essere un servizio meteo, un DMP o persino il tuo servizio web. Puoi utilizzare questi dati per generare tipi di pubblico e contenuti mirati e per arricchire il profilo del visitatore.
audience: marketer
difficulty: 5
author: Daniel Wright
doc-type: use
activity-type: feature-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 40%

---


# Utilizzare i provider di dati per integrare dati di terze parti in  Adobe Target

[!UICONTROL Fornitori di dati è una funzionalità che ti permette di trasmettere facilmente dati da terze parti a Target.  ]  Un esempio di terza parte potrebbe essere un servizio meteo, un DMP o persino il tuo servizio web. Puoi utilizzare questi dati per generare tipi di pubblico e contenuti mirati e per arricchire il profilo del visitatore.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Come utilizzare i provider di dati

1. L&#39;esperto di implementazione aggiunge il codice prima di at.js (o nella sezione Intestazione libreria di at.js) che effettua la chiamata API a terzi, analizza la risposta e specifica con coppie nome/valore dalla risposta da inviare a [!DNL Target].
1. at.js gestisce lo sfarfallio e include le coppie nome/valore come parametri personalizzati nella richiesta di Target globale.
1. Marketer crea audience nell&#39;interfaccia [!DNL Target] in base a questi parametri personalizzati.
1. L&#39;esperto di marketing utilizza queste audience per eseguire il targeting di esperienze, attività e metriche, nonché per il reporting dei tipi di pubblico.

>[!NOTE]
>
>[!UICONTROL I ] provider di dati richiedono at.js 1.3 o versione successiva

## Materiali di supporto

* [Implementa i provider di dati in at.js e  Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
* [Documentazione sui provider di dati](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)