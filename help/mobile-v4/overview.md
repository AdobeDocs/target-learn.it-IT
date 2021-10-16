---
title: Adobe Target con Adobe Mobile Services SDK v4 per Android
description: Adobe Target con Adobe Mobile Services SDK v4 per Android è il punto di partenza ideale per gli sviluppatori Android che utilizzano già Adobe Mobile Services SDK v4 e desiderano iniziare a personalizzare le esperienze delle app con Adobe Target.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile, Overview
doc-type: tutorial
kt: 3040
exl-id: 20f8ed4f-a86d-4c5e-9296-71a93724caa3
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# Adobe Target con Adobe Mobile Services SDK v4 per Android - Panoramica

_Adobe Target con Adobe Mobile Services SDK v4 per_ Android è il punto di partenza ideale per gli sviluppatori Android che utilizzano già Adobe Mobile Services SDK v4 e desiderano iniziare a personalizzare le esperienze delle app con Adobe Target.

È disponibile un’app dimostrativa per Android che consente di completare le lezioni. Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare [!DNL Target] nella tua app Android.

Dopo aver completato questa esercitazione, sarai in grado di:

* Convalida la configurazione [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en)
* Implementa i seguenti tipi di richieste [!DNL Target]:
   * Preacquisizione del contenuto [!DNL Target]
   * Eseguire il batch di più [!DNL Target] posizioni (mbox) in una singola richiesta
   * Richieste di blocco (eseguite prima della visualizzazione dell’app)
   * Richieste non di blocco (eseguite in background)
   * In tempo reale (senza memorizzazione in cache)
   * Recupero cache
* Aggiungere parametri alle richieste di personalizzazione avanzata
* Creare tipi di pubblico e offerte
* Personalizzare i layout
* Implementare nuove funzioni con flag di funzione

## Prerequisiti

In queste lezioni, si presume che tu:

* Disporre di un ID Adobe e di un accesso a livello di approvatore all&#39;interfaccia Adobe Target (consulta i passaggi di verifica seguenti)
* Conosci il tuo codice client Adobe Target in modo da poter effettuare richieste al tuo account. Il codice client viene visualizzato nell’interfaccia di Adobe Target nella sezione   Configurazione > Implementazione > Schermata Modifica impostazioni at.js
* Accedere all&#39; [interfaccia utente di Mobile Services](https://mobilemarketing.adobe.com/) e acquisirne familiarità
* Disporre di un IDE per lo sviluppo di app mobili Android. Questa esercitazione presenta [Android Studio](https://developer.android.com/studio/install) in vari passaggi e schermate

Se non disponi dell&#39;accesso richiesto alle soluzioni Experience Cloud, contatta l&#39;amministratore di Experience Cloud.

Inoltre, si presume che tu abbia familiarità con lo sviluppo Android in Java. Non devi essere un esperto Java per completare le lezioni, ma ti saranno più utili se sei in grado di leggere e comprendere il codice senza difficoltà.

### Verificare l’accesso ad Adobe Target

Questa lezione richiede l’accesso ad Adobe Target. Prima di passare ai passaggi successivi, assicurati di poter accedere ad Adobe Target eseguendo le operazioni seguenti:

1. Accedi a [Adobe Experience Cloud](https://experience.adobe.com/)
1. Dalla schermata iniziale dell’Experience Cloud, fai clic su [!DNL Target]:
   ![Experience Cloud Home Screen](assets/aec_homeScreen_clickTarget.png)
1. Accedi all’elenco Attività in Adobe Target, come illustrato di seguito, e dovresti vedere che il tuo utente dispone dell’accesso a livello di Approvatore. Se non riesci ad accedere a [!DNL Target] o non riesci a verificare l&#39;accesso a livello di Approvatore, contatta uno degli amministratori di Experience Cloud della tua azienda, richiedi questo accesso e riprendi questa esercitazione una volta concesso:

   ![Interfaccia utente Adobe](assets/targetUI_approver.png)

## Informazioni sulle lezioni

In queste lezioni, implementerai Adobe Target in un’app di viaggio dimostrativa denominata &quot;We.Travel&quot; utilizzando il tuo account Adobe Target. Al termine dell’esercitazione, invierai messaggi personalizzati all’utente in base all’utilizzo dell’app. Le esperienze di personalizzazione finali si presenteranno così:

![We.Travel app finale](assets/overview_final_result.jpg)

Dopo aver descritto l’implementazione nell’app We.Travel, potrai iniziare a utilizzare [!DNL Target] nella tua app mobile.

Cominciamo!

**[SUCCESSIVO : &quot;Scarica e aggiorna l’app di esempio&quot; >](download-and-update-the-sample-app.md)**
