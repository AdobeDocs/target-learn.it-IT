---
title: Utilizzare i token di risposta e gli eventi personalizzati at.js con  Adobe Target
seo-title: Utilizzare i token di risposta e gli eventi personalizzati at.js con  Adobe Target
description: I token di risposta e gli eventi personalizzati at.js consentono di condividere le informazioni di profilo da Target a sistemi di terze parti. Qualsiasi oggetto presente nel profilo visitatore Target, inclusi gli attributi di profilo personalizzati, le informazioni geografiche, i dettagli dell'attività e i profili incorporati, può essere aggiunto alla risposta di Target, dove è possibile utilizzare JavaScript personalizzato per l'integrazione con una terza parte.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---


# Utilizzare i token di risposta e gli eventi personalizzati at.js con  Adobe Target

I token di risposta e gli eventi `at.js` personalizzati consentono di condividere le informazioni di profilo da [!DNL Target] sistemi di terze parti. Qualsiasi oggetto presente nel profilo [!DNL Target] visitatore, inclusi gli attributi di profilo personalizzati, le informazioni geografiche, i dettagli dell&#39;attività e i profili incorporati, può essere aggiunto alla [!DNL Target] risposta, dove è possibile utilizzare JavaScript personalizzato per l&#39;integrazione con una terza parte.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Come utilizzare i token di risposta e gli eventi personalizzati at.js

1. Determinare da quali dati ti servono [!DNL Target]
1. Attivate i token di risposta per i dati necessari capovolgendo l&#39;interruttore nella schermata Configurazione->Token di risposta
1. Determinare il listener di eventi da utilizzare
1. Scrivere il codice JavaScript necessario per ascoltare l&#39;evento di Adobe Target , leggere i token di risposta ed eseguire le operazioni necessarie per l&#39;integrazione
1. Implementare il codice JavaScript del listener di eventi utilizzando un&#39;azione di codice personalizzata in Launch dopo l&#39;azione &quot;Carica Target&quot; oppure aggiungerlo alla sezione Library Footer di at.js nella schermata Setup->Implementation e salvare un nuovo file at.js
1. QA e pubblicare l&#39;integrazione

## Risorse aggiuntive

* [Usare il Experience Cloud Debugger con  Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentazione token di risposta](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [Documentazione evento personalizzata At.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Utilizzo di Fornitori di dati in Adobe Target](use-data-providers-to-integrate-third-party-data.md)