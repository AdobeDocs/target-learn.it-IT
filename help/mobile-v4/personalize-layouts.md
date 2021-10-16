---
title: Personalizzare i layout
description: 'In questa lezione finale, creiamo due attività di personalizzazione in Target per il nostro pubblico. Scopri come caricare e visualizzare le attività nell’app e verifica che il contenuto venga visualizzato al momento giusto nelle posizioni giuste.  '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
author: Daniel Wright
exl-id: a9f033d9-9f72-4154-88f5-d36423a404d0
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 1%

---

# Personalizzare i layout

Ora è il momento di mettere tutto insieme e creare esperienze personalizzate. Un _Attività_ è il meccanismo [!DNL Target] che collega le posizioni, i tipi di pubblico e le offerte, in modo che quando la richiesta viene effettuata dall&#39;app, [!DNL Target] risponda con il contenuto personalizzato. Costruiremo due attività di personalizzazione in [!DNL Target] e verificheremo che il contenuto personalizzato venga visualizzato all’utente giusto al momento giusto e nella posizione giusta.

## Obiettivi di apprendimento

Al termine di questa lezione, potrai:

* Creare attività in Adobe Target
* Convalidare le attività nell’app di esempio

## Creare attività in Adobe Target

Scopri come creare attività Coinvolgi utenti e offerte contestuali .

### Prima attività - &quot;Coinvolgere gli utenti&quot;

Di seguito è riportato un riepilogo dell’attività che verrà generata:

| Destinatari | Posizioni | Offerte |
|---|---|---|
| Nuovi utenti delle app mobili | wetravel_Eng_home, wetravel_Eng_search | Home: Coinvolgi nuovi utenti, cerca: Coinvolgi nuovi utenti |
| Restituzione di utenti di app mobili | wetravel_Eng_home, wetravel_Eng_search | Home: Restituire utenti, default_content |

Nell&#39;interfaccia [!DNL Target] procedi come segue:

1. Seleziona **[!UICONTROL Attività]** > **[!UICONTROL Crea attività]** > **[!UICONTROL Targeting esperienza]**.

   ![Crea attività](assets/activity_create_1.jpg)

1. Fai clic su **[!UICONTROL App mobile]**.
1. Selezionare il **[!UICONTROL Compositore modulo]**.
1. Seleziona l’area di lavoro (la stessa area di lavoro utilizzata nelle lezioni precedenti).
1. Seleziona la proprietà (la stessa proprietà utilizzata nelle lezioni precedenti).
1. Fai clic su **[!UICONTROL Successivo]**.

   ![Crea attività](assets/activity_create_2.jpg)

1. Modifica il titolo dell&#39;attività in **[!UICONTROL Coinvolgi utenti]**.
1. Seleziona i **[!UICONTROL puntini di sospensione]** > **[!UICONTROL Cambia pubblico]**.
   ![I nuovi utenti di app mobili cambiano il pubblico](assets/activity_create_3.jpg)
1. Imposta il pubblico su **[!UICONTROL Nuovi utenti di app mobili]**.
1. Fai clic su **[!UICONTROL Fine]**.
   ![Pubblico per utenti di nuove app mobili](assets/activity_create_4.jpg)

1. Cambia la posizione in _wetravel_eng_home_.
1. Seleziona la freccia a discesa accanto a Contenuto predefinito e seleziona **[!UICONTROL Cambia offerta HTML]**.

   ![Pubblico per utenti di nuove app mobili](assets/activity_create_5.jpg)

1. Seleziona la **[!UICONTROL Home: Coinvolgi nuova offerta Utenti]**.
1. Selezionare **[!UICONTROL Fine]**.

   ![Pubblico per utenti di nuove app mobili](assets/activity_create_6.jpg)

1. Seleziona **[!UICONTROL Aggiungi posizione]**.
   ![Pubblico per utenti di nuove app mobili](assets/activity_create_7.jpg)

1. Selezionare la posizione _wetravel_Eng_search_.
1. Modifica l’offerta HTML.

   ![Pubblico per utenti di nuove app mobili](assets/activity_create_8.jpg)

1. Seleziona **[!UICONTROL Cerca: Coinvolgi nuova offerta Utenti]**.
1. Fai clic su **[!UICONTROL Fine]**.

   ![Pubblico per utenti di nuove app mobili](assets/activity_create_9.jpg)

Hai appena connesso un pubblico a posizioni e offerte, creando l’esperienza personalizzata per i nuovi utenti delle app mobili! A questo punto l’esperienza dovrebbe essere simile alla seguente:

![Esperienza Finale](assets/activity_engage_users_a_final.jpg)

Ora crea un’esperienza per la restituzione di utenti di app mobili:

1. Seleziona **[!UICONTROL Aggiungi targeting esperienza]** a sinistra.
1. Seleziona il pubblico **[!UICONTROL Restituzione utenti di app mobili]**.
1. Selezionare **[!UICONTROL Fine]**.
   ![Restituzione del pubblico degli utenti di app mobili](assets/activity_create_11.jpg)

Ora utilizza lo stesso processo utilizzato in precedenza per configurare la nuova esperienza. La configurazione per l’esperienza Restituisci utenti di app mobili dovrebbe essere simile alla seguente:

![Restituzione finale utenti di app mobili](assets/activity_engage_users_b_final.jpg)

Continuiamo alla schermata successiva nella configurazione:

1. Fai clic su **[!UICONTROL Avanti]** per passare alla schermata **[!UICONTROL Targeting]** .
1. Utilizza le impostazioni predefinite per Targeting. Se le esperienze per i tipi di pubblico si sovrappongono (ad esempio _Utenti di New York_ e _Utenti nuovi_) è possibile organizzare l&#39;ordine di priorità in questa schermata.
1. Fai clic su **[!UICONTROL Avanti]** per passare a **[!UICONTROL Obiettivi e impostazioni]**.

   ![Attività Coinvolgi utenti - Impostazione destinazione predefinita](assets/activity_engage_users_targeting.jpg)

Ora completiamo la configurazione dell’attività:

1. Imposta l&#39; **[!UICONTROL Obiettivo primario]** su **[!UICONTROL Conversione]**.
1. Imposta l&#39;azione su **[!UICONTROL Visualizza una mbox]** > _wetravel_context_dest_ (Poiché questa posizione si trova nella schermata di conferma, possiamo usarla per misurare le conversioni).

   ![Attività Coinvolgi utenti - Obiettivi](assets/activity_create_12.jpg)

1. Mantieni tutte le altre impostazioni sullo schermo alle impostazioni predefinite.
1. Fai clic su **[!UICONTROL Salva e chiudi]** per salvare l&#39;attività.
1. Attiva la **[!UICONTROL Attività]** nella schermata successiva.

![Pubblico di Experience B](assets/activity_create_13.jpg)

La nostra prima attività è ora live e pronta per il test!

### Seconda attività - &quot;Offerte contestuali&quot;

Di seguito è riportato un riepilogo della seconda attività che verrà generata:

| Destinatari | Posizione | Offerte |
| --- | --- | --- |
| Destinazione: San Diego | wetravel_context_dest | Promozione a San Diego |
| Destinazione: Los Angeles | wetravel_context_dest | Promozione per Los Angeles |

Ripeti lo stesso processo di cui sopra per l’attività successiva - &quot;Offerte contestuali&quot;. La configurazione finale per entrambe le esperienze è mostrata di seguito:

#### San Diego

![Offerte Contestuali - Esperienza A](assets/activity_contextual_a_final.jpg)

#### Los Angeles

![Offerte contestuali - Esperienza B](assets/activity_contextual_b_final.jpg)

Nel passaggio Obiettivi e impostazioni , l&#39;obiettivo principale verrà modificato nella posizione nella schermata di conferma della prenotazione:

1. In **[!UICONTROL Impostazioni reporting]**, imposta l&#39; **[!UICONTROL Obiettivo primario]** su **[!UICONTROL Conversione]**.
1. Imposta l&#39;azione su **[!UICONTROL Visualizza una mbox]** > _wetravel_context_dest_ (in questa attività, questa metrica è fondamentalmente priva di significato, in quanto è anche la stessa posizione che distribuisce l&#39;esperienza).
1. Fai clic su **[!UICONTROL Salva e chiudi]**.

![Offerte contestuali - Esperienza](assets/activity_create_14.jpg)

Attiva l&#39;attività nella schermata successiva.

Ora la nostra seconda attività è live e pronta per il test!

## Convalidare l’offerta principale

Esegui l’emulatore e controlla che la prima offerta venga visualizzata nella parte inferiore della schermata iniziale. Se sei un utente precedente con 5 o più avvii dell’app, visualizzerai l’offerta _welcome back_ . Se sei un nuovo utente (meno di 5 avvii dell&#39;app), dovresti visualizzare il messaggio _nuovo utente_ :

![Convalida offerta casa](assets/layout_home_validate.jpg)

Se la nuova offerta utente non viene visualizzata, prova a cancellare i dati per il tuo emulatore. In questo modo gli avvii dell’app verranno reimpostati a 1 al successivo avvio. Questa operazione viene eseguita in **[!UICONTROL Strumenti]** > **[!UICONTROL AVD Manager]**. Potrebbe essere necessario riavviare anche Android Studio, se Logcat non funziona correttamente:

![Emulatore a comparsa](assets/layout_home_validate_avd_wipe.jpg)

Puoi anche convalidare la risposta in Logcat filtrando _wetravel_Eng_home_:

![Convalida offerta casa - Logcat](assets/layout_home_validate_logcat.jpg)

## Convalidare l’offerta di ricerca

Seleziona **[!UICONTROL San Jose]** come **[!UICONTROL Partenza]** e **[!UICONTROL San Diego]** come **[!UICONTROL Destinazione]** e fai clic su **[!UICONTROL Trova bus]** per cercare gli autobus disponibili.

Nella schermata dei risultati, dovresti visualizzare il messaggio _use filters_ (usa filtri). Se sei un utente precedente con 5 o più avvii dell’app, non verrà visualizzato alcun messaggio in quanto il contenuto predefinito è impostato per questa posizione (vuoto):

![Convalida offerta ricerca](assets/layout_search_validate.jpg)

## Convalidare le offerte contestuali nella schermata di ringraziamento

Continua ora il processo di prenotazione:

* Seleziona un bus nella schermata dei risultati.
* Selezionare un posto nella schermata di pagamento.
* Seleziona **[!UICONTROL Carta di credito]** nella schermata di pagamento (lascia vuoto il foglio di informazioni di pagamento - non avrà luogo la prenotazione effettiva).

Poiché San Diego è stato selezionato come destinazione, è necessario visualizzare il banner di offerta _DJ SAM_ nella schermata di conferma:

![Convalida offerta contesto - San Diego](assets/layout_context_san_diego.jpg)

Ora seleziona **[!UICONTROL Fine]** e prova un&#39;altra prenotazione con Los Angeles come destinazione. Nella schermata di conferma deve essere visualizzato il banner _Universal Studios_:

![Convalida offerta contesto - Los Angeles](assets/layout_context_los_angeles.jpg)

## Conclusione

Congratulazioni! Questo conclude la parte principale del tutorial Adobe Target SDK 4.x per Android. Ora hai le competenze per implementare la personalizzazione nelle app Android! Puoi fare riferimento a questa documentazione e a questa app demo come riferimento per i tuoi progetti futuri.

Avanti: La funzione di flag delle funzioni è un’altra funzionalità che può essere implementata con Adobe Target in Android. Per informazioni sul flag delle funzioni, consulta la lezione successiva.

**[SUCCESSIVO : Flag delle funzioni >](feature-flagging.md)**
