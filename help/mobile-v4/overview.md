---
title: Adobe Target  con Adobe Mobile Services SDK v4 per Android
description: ' Adobe Target con Adobe Mobile Services SDK v4 per Android è il punto di partenza ideale per gli sviluppatori Android che già utilizzano Adobe Mobile Services SDK v4 e desiderano iniziare a personalizzare le esperienze delle app con  Adobe Target.'
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---


# Panoramica

_Adobe Target con Adobe Mobile Services SDK v4 per Android_ è il punto di partenza ideale per gli sviluppatori Android che già utilizzano Adobe Mobile Services SDK v4 e desiderano iniziare a personalizzare esperienze app con  Adobe Target.

Per completare le lezioni è disponibile un’app demo per Android. Al termine di questa esercitazione, è necessario essere pronti per iniziare a implementare [!DNL Target] nella propria app Android!

Dopo aver completato questa esercitazione, sarai in grado di:

* Convalida dell’impostazione dell’SDK [di](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html) Adobe Mobile Services
* Implementate i seguenti tipi di [!DNL Target] richieste:
   * Preacquisizione del [!DNL Target] contenuto
   * Eseguire il batch di più [!DNL Target] posizioni (mbox) in una singola richiesta
   * Richieste di blocco (eseguite prima della visualizzazione dell&#39;app)
   * Richieste non di blocco (eseguite in background)
   * Real-time (non caching)
   * Recupero cache
* Aggiunta di parametri alle richieste di personalizzazione avanzata
* Creazione di audience e offerte
* Personalizzare i layout
* Nuove funzioni con funzionalità contrassegnate

## Prerequisiti

In queste lezioni si presume che:

* Avere un Adobe ID e un accesso a livello di approver all&#39;interfaccia del Adobe Target  (vedete i passaggi di verifica indicati di seguito)
* Conoscere il codice cliente  Adobe Target in modo da poter effettuare richieste al proprio account. Il Codice client viene visualizzato nell&#39;interfaccia del Adobe Target  nella schermata Configurazione > Implementazione > Modifica impostazioni at.js
* Accedere all&#39;interfaccia utente di [Mobile Services e familiarizzarsi con essa](https://mobilemarketing.adobe.com)
* Disporre di un IDE per lo sviluppo di app mobili Android. Questa esercitazione presenta [Android Studio](https://developer.android.com/studio/install) in vari passaggi e screenshot

Se non disponete dell&#39;accesso necessario alle soluzioni Experience Cloud , rivolgetevi al vostro amministratore Experience Cloud .

Inoltre, si presume che abbiate familiarità con lo sviluppo Android in Java. Non è necessario essere un esperto Java per completare le lezioni, ma si otterrà di più da loro se si può comodamente leggere e capire il codice.

### Verificare l&#39;accesso al Adobe Target 

Questa lezione richiede l&#39;accesso al Adobe Target . Prima di passare ai passaggi successivi, accertatevi di avere accesso  Adobe Target effettuando le seguenti operazioni:

1. Accedi ad [Adobe Experience Cloud](https://experience.adobe.com/)
1. Dalla schermata iniziale  Experience Cloud, fate clic su [!DNL Target]:
   ![Experience Cloud Home Screen](assets/aec_homeScreen_clickTarget.png)
1. Dovresti andare all&#39;elenco Attività in  Adobe Target, come illustrato di seguito, e dovresti vedere che l&#39;utente ha accesso a livello di approver. Se non riuscite ad accedere [!DNL Target] o non riuscite a verificare l&#39;accesso a livello di approver, contattate uno degli amministratori Experience Cloud  della società, richiedete questo accesso e riprendete l&#39;esercitazione una volta concessa:

   ![Adobe UI](assets/targetUI_approver.png)

## Informazioni sulle lezioni

In queste lezioni implementerete  Adobe Target in un&#39;app per viaggi dimostrativi chiamata &quot;We.Travel&quot; utilizzando il vostro account  Adobe Target. Entro la fine dell&#39;esercitazione, invierai agli utenti messaggi personalizzati in base al loro utilizzo dell&#39;app! Le esperienze di personalizzazione finali saranno come segue:

![We.Travel app final](assets/overview_final_result.jpg)

Dopo aver completato l&#39;implementazione nell&#39;app We.Travel potrete iniziare a utilizzare [!DNL Target] nella vostra app mobile.

Cominciamo!

**[NEXT: &quot;Scarica e aggiorna l&#39;app di esempio&quot; >](download-and-update-the-sample-app.md)**