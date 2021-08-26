---
title: Scarica e aggiorna l'app di esempio We.Travel
description: 'L’app di esempio We.Travel è preimplementata con Adobe Mobile Services SDK v4. È sufficiente aggiornarlo in modo che punti ai tuoi account dell''organizzazione Experience Cloud e della soluzione.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: a6b645b6d9693a4c8882fd47ee0d61698c0b834d
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Scarica e aggiorna l&#39;app di esempio We.Travel

L’app di esempio We.Travel è preimplementata con Adobe Mobile Services SDK v4. È sufficiente aggiornarlo in modo che punti ai tuoi account dell&#39;organizzazione di Experience Cloud e della soluzione.

## Obiettivi di apprendimento

Al termine di questa lezione, potrai:

* Scarica e apri l’app di esempio We.Travel in Android Studio.
* Verifica e aggiorna le impostazioni SDK di Mobile Services per [!DNL Target]

## Scarica l&#39;app We.Travel

* Scarica [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Decomprimi il file zip
* Apri l’app in Android Studio come progetto esistente (ignora eventuali errori relativi a &quot;Mappatura radice VCS non valida&quot;)
* Esegui l’app in un emulatore per confermare che l’app sia stata generata e puoi visualizzare la schermata iniziale
* Sfoglia l&#39;app e verifica di poter completare la procedura di prenotazione (seleziona qualsiasi opzione di pagamento e premi semplicemente &quot;Procedi&quot; per saltare la schermata di fatturazione!)

   ![Apri la schermata ](assets/wetravel_homeScreen.png)![appConfirmation .](assets/wetravel_confirmationScreen.png)

## Verifica e aggiorna le impostazioni SDK di Mobile Services per [!DNL Target]

L&#39;SDK di Adobe Mobile Services è stato preinstallato nell&#39;app We.Travel [in base alla documentazione](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en). Ora aggiornerai l’installazione per puntare al tuo account [!DNL Target].

Innanzitutto, crea una nuova app nell’interfaccia utente di Mobile Services:

1. Accedi all&#39; [interfaccia Adobe Mobile Services](https://mobilemarketing.adobe.com).
1. Vai a [!UICONTROL Gestione app], quindi fai clic su **[!UICONTROL Aggiungi]** per aggiungere una nuova app da utilizzare con questa esercitazione (**[!UICONTROL Gestione app]** > **[!UICONTROL Aggiungi]**).
1. Scegli una suite di rapporti di Analytics con dati non di produzione, assegna un nome all’app, seleziona il tipo **[!UICONTROL Standard]** e fai clic su **[!UICONTROL Salva]**.
1. Una volta aggiunta l&#39;app, aggiungi il tuo [!DNL Target] Codice client nella schermata successiva nella sezione [!UICONTROL Opzioni SDK Target] (puoi trovare il tuo codice client nell&#39;interfaccia [!DNL Target] in **[!UICONTROL Configurazione]** > **[!UICONTROL Implementazione]** > **[!UICONTROL Modifica impostazioni]**, accanto al download `at.js`).
1. L&#39;impostazione [!UICONTROL Timeout richiesta] determina per quanto tempo l&#39;app attende la risposta dal server [!DNL Target] prima di eseguire le istruzioni di timeout. Lascia l’impostazione predefinita.
1. Abilita il [!UICONTROL Servizio ID visitatore] e assicurati che la tua [!UICONTROL Organizzazione] sia selezionata nel menu a discesa.
1. Salva le modifiche facendo clic su **[!UICONTROL Salva]** in alto a destra nella finestra (non su quella nella sezione [!UICONTROL Collegamenti universali], [!UICONTROL Collegamenti app] o [!UICONTROL Servizi push] ).
1. Scorri fino alla sezione Download di SDK per app nella parte inferiore della pagina e scarica il file di configurazione:

   ![Scarica il file di configurazione](assets/config_file.jpg)

1. Sostituisci il file `ADBMobileConfig.json` nella cartella delle risorse del progetto Android Studio (app > src > main > assets).

1. Ora apri il file `ADBMobileConfig.json` e accertati che contenga le modifiche previste, ad esempio il codice client [!DNL Target] e i dettagli di Analytics:
   ![Scarica il file di configurazione](assets/client_code.jpg)

Se non trovi le impostazioni, conferma di aver fatto clic sul pulsante **[!UICONTROL Salva]** destro nell&#39;interfaccia [!UICONTROL Mobile Services] e di aver copiato il file nella posizione corretta.

Congratulazioni! Hai aggiornato l&#39;SDK con i tuoi [!DNL Target] dettagli account! Dopo l’aggiunta delle richieste [!DNL Target] nella lezione successiva effettueremo un’ulteriore convalida della configurazione.

**[SUCCESSIVO : &quot;Aggiungi richieste Target&quot; >](add-requests.md)**
