---
title: Flag delle funzioni
description: Adobe Target può essere utilizzato per sperimentare funzioni UX come colore, copia, pulsanti, testo e immagini e fornire tali funzionalità a tipi di pubblico specifici.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---


# Flag delle funzioni

I proprietari di app mobili hanno bisogno della flessibilità necessaria per implementare nuove funzionalità nella loro app senza dover investire in più versioni di app. Possono anche voler distribuire gradualmente le funzionalità a una percentuale della base utente, per testare l&#39;efficacia. Adobe Target può essere utilizzato per sperimentare funzioni UX come colore, copia, pulsanti, testo e immagini e fornire tali funzionalità a tipi di pubblico specifici.

In questa lezione verrà creata un’offerta con flag di funzione che può essere utilizzata come attivatore per abilitare funzioni specifiche dell’app.

## Obiettivi di apprendimento

Al termine di questa lezione, potrai:

* Aggiungi una nuova posizione alla richiesta di recupero preventivo del batch
* Crea un’attività [!DNL Target] con un’offerta che verrà utilizzata come flag di funzione
* Carica e convalida l’offerta con flag di funzione nell’app.

## Aggiungi una nuova posizione alla richiesta di preacquisizione all’attività principale

Nell’app dimostrativa delle nostre lezioni precedenti, aggiungeremo una nuova posizione denominata &quot;wetravel_feature_flag_recs&quot; alla richiesta di preacquisizione nell’attività iniziale e la caricheremo sullo schermo con un nuovo metodo Java.

>[!NOTE]
>
>Uno dei vantaggi dell’utilizzo di una richiesta di preacquisizione è che l’aggiunta di una nuova richiesta non aggiunge un sovraccarico di rete aggiuntivo o causa un carico aggiuntivo poiché la richiesta viene inclusa nella richiesta di preacquisizione

In primo luogo, verifica che la costante wetravel_feature_flag_recs sia aggiunta nel file Constant.java:

![Aggiungi costante flag di funzione](assets/feature_flag_constant.jpg)

Ecco il codice:

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

Ora aggiungi la posizione alla richiesta di preacquisizione e carica una nuova funzione chiamata `processFeatureFlags()`:

![Codice contrassegno funzione](assets/feature_flag_code.jpg)

Di seguito è riportato il codice aggiornato completo:

```java
public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();

    Map<String, Object> params1;
    params1 = new HashMap<String, Object>();
    params1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");

    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_feature_flag_recs, params1));

    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    engageMessage();
                    processFeatureFlags();
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}

public void processFeatureFlags() {
    Target.loadRequest(Constant.wetravel_feature_flag_recs, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Feature Flags : " + s);
                            if(s != null && !s.isEmpty()) {
                                //enable or disable features
                            }
                        }
                    });
                }
            });
}
```

### Convalida la richiesta di flag di funzione

Una volta aggiunto il codice, esegui l’emulatore sull’attività principale e controlla Logcat per la risposta aggiornata:

![Convalida posizione flag caratteristica](assets/feature_flag_code_logcat.jpg)

## Creare un’offerta JSON con flag di funzione

Ora creeremo una semplice offerta JSON che fungerà da flag o attivatore per un pubblico specifico, il pubblico che riceverà il rollout delle funzioni nella loro app. Nell’interfaccia [!DNL Target] , crea una nuova offerta:

![Creare un’offerta JSON con flag di funzione](assets/feature_flag_json_offer.jpg)

Chiamiamolo &quot;Flag di funzionalità v1&quot; con il valore {&quot;enable&quot;:1}

![offerta JSON feature_flag_v1](assets/feature_flag_json_name.jpg)

## Creazione di un&#39;attività

Ora creiamo un’attività Test A/B con quell’offerta. Per i passaggi dettagliati sulla creazione di un’attività, consulta la lezione precedente. Per questo esempio, l’attività avrà bisogno di un solo pubblico. In uno scenario live, puoi creare tipi di pubblico personalizzati specifici per specifici rollout di funzioni, quindi impostare l’attività per l’utilizzo di tali tipi di pubblico. In questo esempio, alloceremo il traffico 50/50 (50% per i visitatori che visualizzano gli aggiornamenti di funzionalità e 50% per i visitatori che visualizzano un’esperienza standard). Ecco la configurazione dell’attività:

1. Denomina l&#39;attività &quot;Flag di funzionalità&quot;
1. Selezionare la posizione &quot;wetravel_feature_flag_recs&quot;
1. Modifica il contenuto dell’offerta JSON &quot;Flag di funzione v1&quot;

   ![Configurazione dell’attività del flag funzione](assets/feature_flag_activity.jpg)

1. Fai clic su **[!UICONTROL Aggiungi esperienza]** per aggiungere l&#39;esperienza B.
1. Lascia la posizione &quot;wetravel_feature_flag_recs&quot;
1. Lascia **[!UICONTROL Contenuto predefinito]** per il contenuto
1. Fai clic su **[!UICONTROL Avanti]** per passare alla schermata [!UICONTROL Targeting]

   ![Configurazione dell’attività del flag funzione](assets/feature_flag_activity_2.jpg)

1. Nella schermata [!UICONTROL Targeting] , verifica che il metodo [!UICONTROL Allocazione traffico] sia impostato sull&#39;impostazione predefinita (Manuale) e che ogni esperienza abbia l&#39;allocazione predefinita del 50%. Seleziona **[!UICONTROL Avanti]** per passare a **[!UICONTROL Obiettivi e impostazioni]**.

   ![Configurazione dell’attività del flag funzione](assets/feature_flag_activity_3.jpg)

1. Imposta l&#39; **[!UICONTROL Obiettivo primario]** su **[!UICONTROL Conversione]**.
1. Imposta l&#39;azione su **[!UICONTROL Visualizzato un mbox]**. Useremo la posizione &quot;wetravel_context_dest&quot; (poiché questa posizione si trova nella schermata di conferma, possiamo usarla per vedere se la nuova funzione porta a più conversioni).
1. Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![Configurazione dell’attività del flag funzione](assets/feature_flag_activity_4.jpg)

Attivare l&#39;attività.

## Convalidare l’attività del flag di funzione

Ora utilizza l’emulatore per controllare la richiesta. Poiché il targeting è stato impostato sul 50% degli utenti, il 50% della risposta del flag di funzione contiene il valore `{enable:1}`.

![Convalida del flag della funzione](assets/feature_flag_validation.jpg)

Se il valore `{enable:1}` non viene visualizzato, significa che non è stato eseguito il targeting per l’esperienza. Come test temporaneo, per forzare la visualizzazione dell’offerta, puoi:

1. Disattiva l’attività.
1. Modifica l’allocazione del traffico al 100% sulla nuova esperienza di funzionalità.
1. Salva e riattiva.
1. Cancella i dati sull&#39;emulatore e quindi riavvia l&#39;app.
1. L’offerta deve ora restituire il valore `{enable:1}` .

In uno scenario live, la risposta `{enable:1}` può essere utilizzata per abilitare una logica più personalizzata nell&#39;app per visualizzare il set di funzioni specifico che desideri mostrare al pubblico di destinazione.

## Conclusione

Ottimo lavoro! Ora disponi delle competenze necessarie per distribuire funzionalità a tipi di pubblico specifici.
