---
title: Personalizzazione dei layout
description: In questa lezione finale, creiamo due attività di personalizzazione in Target per i nostri tipi di pubblico. Scopri come caricare e visualizzare le attività nell’app e verificare che il contenuto venga visualizzato al momento giusto nelle posizioni giuste.
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
source-wordcount: '992'
ht-degree: 0%

---

# Personalizzazione dei layout

Ora è il momento di mettere insieme tutto e creare esperienze personalizzate. Un&#39;_attività_ è il meccanismo [!DNL Target] che collega le posizioni, i tipi di pubblico e le offerte, in modo che quando la richiesta viene effettuata dall&#39;app, [!DNL Target] risponda con il contenuto personalizzato. Creeremo due attività di personalizzazione in [!DNL Target] e confermeremo che il contenuto personalizzato venga visualizzato all&#39;utente giusto al momento giusto e nella posizione giusta.

## Finalità di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Creare attività in Adobe Target
* Convalidare le attività nell’app di esempio

## Creare attività in Adobe Target

Scopri come creare attività Coinvolgi utenti e Offerte contestuali.

### Prima attività: &quot;Coinvolgere gli utenti&quot;

Ecco un riepilogo dell’attività che creeremo:

| Destinatari | Posizioni | Offerte |
|---|---|---|
| Nuovi utenti di app mobili | wetravel_engagement_home, wetravel_eng_search | Home: Coinvolgi nuovi utenti, Ricerca: Coinvolgi nuovi utenti |
| Restituzione degli utenti di app mobili | wetravel_engagement_home, wetravel_eng_search | Home: Utenti di ritorno, default_content |

Nell&#39;interfaccia [!DNL Target] eseguire le operazioni seguenti:

1. Selezionare **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]**.

   ![Crea attività](assets/activity_create_1.jpg)

1. Fare clic su **[!UICONTROL Mobile App]**.
1. Selezionare **[!UICONTROL Form composer]**.
1. Seleziona l’area di lavoro (la stessa utilizzata nelle lezioni precedenti).
1. Seleziona la Proprietà (la stessa proprietà utilizzata nelle lezioni precedenti).
1. Fare clic su **[!UICONTROL Next]**.

   ![Crea attività](assets/activity_create_2.jpg)

1. Cambia il titolo dell&#39;attività in **[!UICONTROL Engage Users]**.
1. Selezionare **[!UICONTROL ellipsis]** > **[!UICONTROL Change Audience]**.
   ![Il Pubblico Cambia Per I Nuovi Utenti Dell&#39;App Mobile](assets/activity_create_3.jpg)
1. Imposta il pubblico su **[!UICONTROL New Mobile App Users]**.
1. Fare clic su **[!UICONTROL Done]**.
   ![Pubblico nuovi utenti app mobili](assets/activity_create_4.jpg)

1. Cambia il percorso in _wetravel_eng_home_.
1. Selezionare la freccia a discesa accanto a Contenuto predefinito e selezionare **[!UICONTROL Change HTML Offer]**.

   ![Pubblico nuovi utenti app mobili](assets/activity_create_5.jpg)

1. Selezionare l&#39;offerta **[!UICONTROL Home: Engage New Users]**.
1. Selezionare **[!UICONTROL Done]**.

   ![Pubblico nuovi utenti app mobili](assets/activity_create_6.jpg)

1. Selezionare **[!UICONTROL Add Location]**.
   ![Pubblico nuovi utenti app mobili](assets/activity_create_7.jpg)

1. Seleziona il percorso _wetravel_eng_search_.
1. Modifica l’offerta HTML.

   ![Pubblico nuovi utenti app mobili](assets/activity_create_8.jpg)

1. Selezionare l&#39;offerta **[!UICONTROL Search: Engage New Users]**.
1. Fare clic su **[!UICONTROL Done]**.

   ![Pubblico nuovi utenti app mobili](assets/activity_create_9.jpg)

Hai appena collegato un pubblico a posizioni e offerte, creando un’esperienza personalizzata per i nuovi utenti dell’app mobile. Ora l’esperienza dovrebbe essere simile alla seguente:

![Esperienza Finale](assets/activity_engage_users_a_final.jpg)

Ora crea un’esperienza per gli utenti di ritorno dell’app mobile:

1. Selezionare **[!UICONTROL Add Experience Targeting]** a sinistra.
1. Selezionare il pubblico **[!UICONTROL Returning Mobile App Users]**.
1. Selezionare **[!UICONTROL Done]**.
   ![Restituzione pubblico utenti app mobile](assets/activity_create_11.jpg)

Ora utilizza lo stesso processo utilizzato in precedenza per configurare la nuova esperienza. La configurazione per l’esperienza Utenti app mobili di ritorno sarà simile alla seguente:

![Restituzione utenti finali app mobile](assets/activity_engage_users_b_final.jpg)

Passiamo alla schermata successiva nella configurazione:

1. Fare clic su **[!UICONTROL Next]** per passare alla schermata **[!UICONTROL Targeting]**.
1. Utilizza le impostazioni predefinite per il targeting. Se hai esperienze per tipi di pubblico sovrapposti (ad esempio _Utenti New York_ e _Utenti nuovi_) puoi ordinare l&#39;ordine di priorità in questa schermata.
1. Fare clic su **[!UICONTROL Next]** per passare a **[!UICONTROL Goals & Settings]**.

   ![Coinvolgi l&#39;attività degli utenti - Impostazione predefinita del targeting](assets/activity_engage_users_targeting.jpg)

Ora completiamo la configurazione dell’attività:

1. Imposta **[!UICONTROL Primary Goal]** su **[!UICONTROL Conversion]**.
1. Imposta l&#39;azione su **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (poiché questa posizione si trova nella schermata di conferma, è possibile utilizzarla per misurare le conversioni).

   ![Coinvolgi l&#39;attività degli utenti - Obiettivi](assets/activity_create_12.jpg)

1. Mantenere tutte le altre impostazioni sullo schermo sui valori predefiniti.
1. Fare clic su **[!UICONTROL Save & Close]** per salvare l&#39;attività.
1. Attiva **[!UICONTROL Activity]** nella schermata successiva.

![Pubblico Experience B](assets/activity_create_13.jpg)

La nostra prima attività è ora live e pronta per essere testata.

### Seconda attività: &quot;Offerte contestuali&quot;

Ecco un riepilogo della seconda attività che creeremo:

| Destinatari | Posizione | Offerte |
| --- | --- | --- |
| Destinazione: San Diego | wetravel_context_dest | Promozione per San Diego |
| Destinazione: Los Angeles | wetravel_context_dest | Promozione per Los Angeles |

Ripeti lo stesso processo descritto in precedenza per l’attività successiva, &quot;Offerte contestuali&quot;. Di seguito è illustrata la configurazione finale per entrambe le esperienze:

#### San Diego

![Offerte contestuali - Esperienza A](assets/activity_contextual_a_final.jpg)

#### Los Angeles

![Offerte contestuali - Esperienza B](assets/activity_contextual_b_final.jpg)

Nel passaggio Obiettivi e impostazioni, modificheremo l’obiettivo principale nella posizione indicata nella schermata di conferma della prenotazione:

1. In **[!UICONTROL Reporting Settings]**, impostare **[!UICONTROL Primary Goal]** su **[!UICONTROL Conversion]**.
1. Imposta l&#39;azione su **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (in questa attività questa metrica è sostanzialmente priva di significato, poiché si tratta anche della stessa posizione che distribuisce l&#39;esperienza).
1. Fare clic su **[!UICONTROL Save & Close]**.

![Offerte contestuali - Esperienza](assets/activity_create_14.jpg)

Attiva l&#39;attività nella schermata successiva.

Ora la nostra seconda attività è live e pronta per essere testata.

## Convalidare l’offerta iniziale

Esegui l’emulatore e osserva la prima offerta da visualizzare nella parte inferiore della schermata iniziale. Se sei un utente di ritorno con 5 o più avvii di app, vedrai l&#39;offerta _bentornato_ visualizzata. Se sei un nuovo utente (meno di 5 avvii di app), dovresti visualizzare il messaggio _nuovo utente_:

![Convalida offerta principale](assets/layout_home_validate.jpg)

Se la nuova offerta utente non viene visualizzata, prova a cancellare i dati per l’emulatore. In questo modo al prossimo avvio l&#39;app verrà reimpostata su 1. Operazione eseguita in **[!UICONTROL Tools]** > **[!UICONTROL AVD Manager]**. Se Logcat non funziona correttamente, potrebbe essere necessario riavviare anche Android Studio:

![Emulatore cancellazione dati](assets/layout_home_validate_avd_wipe.jpg)

Puoi anche convalidare la risposta in Logcat filtrando per _wetravel_eng_home_:

![Convalida offerta iniziale - Logcat](assets/layout_home_validate_logcat.jpg)

## Convalidare l’offerta di ricerca

Seleziona **[!UICONTROL San Jose]** come **[!UICONTROL Departure]** e **[!UICONTROL San Diego]** come **[!UICONTROL Destination]** e fai clic su **[!UICONTROL Find Bus]** per cercare i bus disponibili.

Nella schermata dei risultati dovrebbe essere visualizzato il messaggio _usa filtri_. Se sei un utente di ritorno con 5 o più avvii di app, non verrà visualizzato alcun messaggio qui, poiché per questa posizione è impostato il contenuto predefinito (che è vuoto):

![Convalida offerta di ricerca](assets/layout_search_validate.jpg)

## Convalidare le offerte contestuali nella schermata di ringraziamento

Continuare ora il processo di prenotazione:

* Selezionare un bus nella schermata dei risultati.
* Selezionare un posto nella schermata di pagamento.
* Seleziona **[!UICONTROL Credit Card]** nella schermata di pagamento (lascia vuote le informazioni sul pagamento; non verrà effettuata alcuna prenotazione effettiva).

Poiché San Diego è stata selezionata come destinazione, nella schermata di conferma dovrebbe essere visualizzato il banner dell&#39;offerta _DJ SAM_:

![Convalida offerta contesto - San Diego](assets/layout_context_san_diego.jpg)

Selezionare **[!UICONTROL Done]** e provare un&#39;altra prenotazione con Los Angeles come destinazione. Nella schermata di conferma verrà visualizzato il banner _Universal Studios_:

![Convalida offerta contesto - Los Angeles](assets/layout_context_los_angeles.jpg)

## Conclusione

Congratulazioni! In questo modo si conclude la parte principale dell’esercitazione Adobe Target SDK 4.x per Android. Ora disponi delle competenze necessarie per implementare la personalizzazione nelle app Android. Consulta questa documentazione e app demo come riferimento per i tuoi progetti futuri.

Successivo: l’assegnazione di un flag a una funzione è un’altra funzione che può essere implementata con Adobe Target in Android. Per informazioni sui contrassegni di funzionalità, consulta la lezione successiva.

**[AVANTI: segnalazione funzionalità >](feature-flagging.md)**
