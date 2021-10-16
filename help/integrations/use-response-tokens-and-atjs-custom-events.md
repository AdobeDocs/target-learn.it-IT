---
title: Come utilizzare i token di risposta e gli eventi personalizzati at.js
description: Scopri come utilizzare i token di risposta e gli eventi personalizzati at.js per condividere le informazioni sul profilo da Target a sistemi di terze parti.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 3%

---

# Utilizza i token di risposta e gli eventi personalizzati at.js con Adobe Target

I token di risposta e gli `at.js` eventi personalizzati ti consentono di condividere informazioni sul profilo da [!DNL Target] a sistemi di terze parti. Qualsiasi oggetto nel profilo visitatore [!DNL Target], inclusi gli attributi di profilo personalizzati, le informazioni geografiche, i dettagli dell’attività e i profili incorporati, può essere aggiunto alla risposta [!DNL Target] in cui puoi utilizzare JavaScript personalizzato per l’integrazione con una terza parte.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Come utilizzare i token di risposta e gli eventi personalizzati at.js

1. Determinare i dati necessari da [!DNL Target]
1. Attiva i token di risposta per i dati necessari capovolgendo l&#39;interruttore sulla schermata Configurazione->Token di risposta
1. Determinare il listener di eventi da utilizzare
1. Scrivi il JavaScript necessario per ascoltare l’evento Adobe Target, leggere i token di risposta e fare ciò che ti serve per la tua integrazione
1. Distribuisci JavaScript del listener di eventi utilizzando un&#39;azione di codice personalizzato in Launch dopo l&#39;azione &quot;Load Target&quot; oppure aggiungilo alla sezione Library Footer di at.js nella schermata Configurazione->Implementazione e salva un nuovo file at.js
1. Controllo qualità e pubblicazione dell’integrazione

## Risorse aggiuntive

* [Utilizzare il Experience Cloud Debugger con Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentazione sul token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Documentazione evento personalizzata at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/atjs-custom-events.html?lang=en)
* [Utilizzo di Fornitori di dati in Adobe Target](use-data-providers-to-integrate-third-party-data.md)
