---
title: Scarica e aggiorna l'app di esempio We.Travel
seo-title: Scarica l’app di esempio e verifica l’SDK dei servizi mobili
description: 'L’app di esempio We.Travel è preimplementata con l’SDK v4  Adobe Mobile Services. È sufficiente aggiornarlo in modo che punti al tuo  Experience Cloud di organizzazione e account della soluzione.   '
seo-description: L’app di esempio We.Travel è preimplementata con l’SDK v4  Adobe Mobile Services. È sufficiente aggiornarlo in modo che punti al tuo  Experience Cloud di organizzazione e account della soluzione.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Scarica e aggiorna l&#39;app di esempio We.Travel

L’app di esempio We.Travel è preimplementata con l’SDK v4  Adobe Mobile Services. È sufficiente aggiornarla, in modo che punti all&#39;organizzazione  Experience Cloud e agli account della soluzione.

## Obiettivi di apprendimento

Al termine di questa lezione, potrete:

* Scarica e apri l&#39;app di esempio We.Travel in Android Studio
* Verifica e aggiorna le impostazioni SDK di Mobile Services per [!DNL Target]

## Scarica l&#39;app We.Travel

* Scarica l’ [esempio-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Decomprimi il file zip
* Apri l&#39;app in Android Studio come progetto esistente (ignora eventuali errori relativi alla &quot;Mappatura radice VCS non valida&quot;)
* Eseguite l&#39;app in un emulatore per confermare che l&#39;app sia stata creata e che sia possibile visualizzare la schermata iniziale
* Sfoglia l&#39;app e verifica di poter completare la procedura di prenotazione (seleziona qualsiasi opzione di pagamento e fai clic su &quot;Procedi&quot; per saltare la schermata di fatturazione!)

   ![Aprite la schermata](assets/wetravel_homeScreen.png)![appConfirm](assets/wetravel_confirmationScreen.png)

## Verifica e aggiorna le impostazioni SDK di Mobile Services per [!DNL Target]

 Adobe Mobile Services SDK è stato preinstallato nell&#39;app We.Travel [in base alla documentazione](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). A questo punto, aggiornerete l&#39;installazione in modo che punti al vostro [!DNL Target] account personale.

Innanzitutto, crea una nuova app nell&#39;interfaccia utente di Mobile Services:

1. Log in to the [Adobe Mobile Services interface](https://mobilemarketing.adobe.com).
1. Andate a [!UICONTROL Gestione app], quindi fate clic su **[!UICONTROL Aggiungi]** per aggiungere una nuova app da utilizzare con questa esercitazione (**[!UICONTROL Gestisci app]** > **[!UICONTROL Aggiungi]**).
1. Scegliete una suite di rapporti Analytics  con dati non di produzione, assegnate all&#39;app un nome, selezionate il tipo **[!UICONTROL Standard]** e fate clic su **[!UICONTROL Salva]**.
1. Una volta aggiunta l&#39;app, aggiungi il tuo Codice [!DNL Target] cliente nella schermata successiva nella sezione Opzioni [!UICONTROL Target] SDK (puoi trovare il codice client nell&#39; [!DNL Target] interfaccia in **[!UICONTROL Configurazione]** > **[!UICONTROL Implementazione]** > **[!UICONTROL Modifica impostazioni]**`at.js` , accanto al pulsante Scarica).
1. L&#39;impostazione Timeout  richiesta determina per quanto tempo l&#39;app attende la risposta dal [!DNL Target] server prima di eseguire le istruzioni sul timeout. Lasciate solo l&#39;impostazione predefinita.
1. Abilita il servizio [!UICONTROL ID] visitatore e accertati che l’ [!UICONTROL organizzazione] sia selezionata nell’elenco a discesa.
1. Per salvare le modifiche, fai clic su **[!UICONTROL Salva]** in alto a destra nella finestra (non nella sezione Collegamenti universali, Collegamenti  app o Servizi  push).
1. Scorri fino alla sezione Download di SDK per app nella parte inferiore della pagina e scarica il file di configurazione:

   ![Scaricare il file di configurazione](assets/config_file.jpg)

1. Sostituisci il `ADBMobileConfig.json` file nella cartella delle risorse del progetto Android Studio (app > src > main > assets).

1. Ora aprite il `ADBMobileConfig.json` file e accertatevi che contenga le modifiche previste, ad esempio il codice [!DNL Target] client e i dettagli Analytics :
   ![Scaricare il file di configurazione](assets/client_code.jpg)

Se non trovi le impostazioni, conferma di aver fatto clic sul pulsante **[!UICONTROL Salva]** destro nell&#39;interfaccia di [!UICONTROL Mobile Services] e di aver copiato il file nella posizione corretta.

Congratulazioni! Hai aggiornato l’SDK con i dettagli del tuo [!DNL Target] account! Dopo aver aggiunto [!DNL Target] le richieste nella lezione successiva, effettueremo una convalida aggiuntiva della configurazione.

**[NEXT: &quot;Aggiungi richieste Target&quot; >](add-requests.md)**
