---
title: Come utilizzare i token di risposta e gli eventi personalizzati at.js
description: Scopri come utilizzare i token di risposta e gli eventi personalizzati at.js per condividere le informazioni del profilo da Target a sistemi di terze parti.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 3%

---

# Utilizzare i token di risposta e gli eventi personalizzati at.js con Adobe Target

I token di risposta e `at.js` eventi personalizzati consentono di condividere le informazioni del profilo da [!DNL Target] a sistemi di terze parti. Qualsiasi oggetto nel profilo visitatore di [!DNL Target], inclusi gli attributi di profilo personalizzati, le informazioni geografiche, i dettagli dell&#39;attività e i profili incorporati, può essere aggiunto alla risposta di [!DNL Target] dove è possibile utilizzare JavaScript personalizzato per l&#39;integrazione con una terza parte.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Come utilizzare i token di risposta e gli eventi personalizzati at.js

1. Determinare i dati necessari da [!DNL Target]
1. Attiva i token di risposta per i dati necessari capovolgendo l’interruttore nella schermata Configurazione->Token di risposta
1. Determinare il listener di eventi da utilizzare
1. Scrivere il JavaScript necessario per ascoltare l’evento Adobe Target, leggere i token di risposta ed eseguire le operazioni necessarie per l’integrazione
1. Distribuisci il listener di eventi JavaScript utilizzando un’azione di codice personalizzato in Launch dopo l’azione &quot;Load Target&quot; oppure aggiungilo alla sezione Library Footer di at.js nella schermata Setup->Implementation e salva un nuovo file at.js
1. Controllo qualità e pubblicazione dell’integrazione

## Risorse aggiuntive

* [Utilizzare Experience Cloud Debugger con Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentazione del token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Utilizzo di Fornitori di dati in Adobe Target](use-data-providers-to-integrate-third-party-data.md)
