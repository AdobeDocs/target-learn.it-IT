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
TQID: https://experienceleague.adobe.com/gJfFi9mC3iKY8pEdvE1Tuk7Mk2rUOdTKtv67vXQwkO8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 3%

---

# Utilizzare i token di risposta e gli eventi personalizzati at.js con Adobe Target

I token di risposta e `at.js` eventi personalizzati consentono di condividere le informazioni del profilo da [!DNL Target] a sistemi di terze parti. Qualsiasi oggetto nel profilo visitatore di [!DNL Target], inclusi gli attributi di profilo personalizzati, le informazioni geografiche, i dettagli dell&#39;attività e i profili incorporati, può essere aggiunto alla risposta di [!DNL Target] dove è possibile utilizzare JavaScript personalizzato per l&#39;integrazione con una terza parte.

>[!VIDEO](https://video.tv.adobe.com/v/326685/?captions=ita&quality=12)

## Come utilizzare i token di risposta e gli eventi personalizzati at.js

1. Determinare i dati necessari da [!DNL Target]
1. Attiva i token di risposta per i dati necessari capovolgendo l’interruttore nella schermata Configurazione->Token di risposta
1. Determinare il listener di eventi da utilizzare
1. Scrivere il JavaScript necessario per ascoltare l’evento Adobe Target, leggere i token di risposta ed eseguire le operazioni necessarie per l’integrazione
1. Distribuisci il listener di eventi JavaScript utilizzando un’azione di codice personalizzato in Launch dopo l’azione &quot;Load Target&quot; oppure aggiungilo alla sezione Library Footer di at.js nella schermata Setup->Implementation e salva un nuovo file at.js
1. Controllo qualità e pubblicazione dell’integrazione

## Risorse aggiuntive

* [Utilizzare Experience Cloud Debugger con Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentazione del token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=it)
* [Utilizzo di Fornitori di dati in Adobe Target](use-data-providers-to-integrate-third-party-data.md)
