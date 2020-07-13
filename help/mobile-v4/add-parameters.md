---
title: Aggiungere parametri alle richieste
description: In questa lezione verranno aggiunte le metriche del ciclo di vita di Adobe e i parametri personalizzati alle richieste Target aggiunte nella lezione precedente. Tali metriche e parametri verranno utilizzati per creare audience personalizzate più avanti nell'esercitazione.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: 199fbde58696a0511623c5500cc6afbbcfdd67a3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Aggiungere parametri alle richieste

In questa lezione verranno aggiunte le metriche del ciclo di vita di Adobe e i parametri personalizzati alle [!DNL Target] richieste aggiunte nella lezione precedente. Tali metriche e parametri verranno utilizzati per creare audience personalizzate più avanti nell&#39;esercitazione.

## Obiettivi di apprendimento

Al termine di questa lezione, potrete:

* Aggiungere le metriche del ciclo di vita di Adobe Mobile
* Aggiunta di parametri a una richiesta di preacquisizione
* Aggiunta di parametri a una posizione live
* Convalida dei parametri per entrambe le richieste

## Aggiungere i parametri del ciclo di vita

Consentiamo le metriche [del ciclo di vita di](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.html)Adobe Mobile. In questo modo verranno aggiunti parametri alle richieste di posizione contenenti informazioni dettagliate sul dispositivo dell&#39;utente e sul coinvolgimento con l&#39;app. Creeremo audience nella lezione successiva utilizzando i dati forniti dalla richiesta del ciclo di vita.

Per abilitare le metriche del ciclo di vita, apri di nuovo il controller HomeActivity e aggiungi `Config.collectLifecycleData(this);` alla funzione onResume():

![Richiesta del ciclo di vita](assets/lifecycle_code.jpg)

### Convalida dei parametri del ciclo di vita per la richiesta di recupero preventivo

Eseguire l&#39;emulatore e utilizzare Logcat per convalidare i parametri del ciclo di vita. Filtra per &quot;preacquisizione&quot; per trovare la risposta di preacquisizione e cercare i nuovi parametri:
![Convalida del ciclo di vita](assets/lifecycle_validation.jpg)

Anche se abbiamo aggiunto solo `Config.collectLifecycleData()` al controller HomeActivity, anche le metriche del ciclo di vita inviate con la richiesta Target devono essere visualizzate nella schermata di ringraziamento.

## Aggiungete il parametro at_property alla richiesta di recupero preventivo

 Proprietà Adobe Target sono definite nell&#39; [!DNL Target] interfaccia e sono utilizzate per stabilire limiti per la personalizzazione di app e siti Web. Il parametro at_property identifica la proprietà specifica in cui le offerte e le attività sono accessibili e mantenute. Aggiungeremo una proprietà alle richieste di preacquisizione e di posizione attiva.

>[!NOTE]
>
>L&#39;utente potrebbe visualizzare o meno le opzioni Proprietà nell&#39; [!DNL Target] interfaccia, a seconda della licenza. Se non disponete di queste opzioni, o se non utilizzate Proprietà nella società, passate alla sezione successiva della lezione.

È possibile recuperare il valore at_property nell’ [!DNL Target] interfaccia in [!UICONTROL Configurazione] > [!UICONTROL Proprietà].  Passate il puntatore del mouse sulla proprietà, selezionate l’icona del frammento di codice e copiate il `at_property` valore:

![Copia at_property](assets/at_property_interface.jpg)

Aggiungetelo come parametro per ogni posizione nella richiesta di preacquisizione, come segue:
![Aggiungere il parametro](assets/params_at_property.jpg)at_property Qui è il codice aggiornato per la `targetPrefetchContent()` funzione (assicurarsi di aggiornare il _[!UICONTROL valore at_property va qui]_il testo segnaposto!):

```java
public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();

        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");

        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();

                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
```

### Nota Sui Parametri

Per i progetti futuri, potrebbe essere utile implementare parametri aggiuntivi. Il `createTargetPrefetchObject()` metodo consente tre tipi di parametri: `locationParams`, `orderParams`e `productParams`. Per [ulteriori dettagli sull’aggiunta di questi parametri alla richiesta](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html)di recupero preventivo, consultate la documentazione.

È inoltre possibile aggiungere parametri di posizione diversi a ogni posizione nella richiesta di preacquisizione. Ad esempio, potete creare un’altra Mappa denominata param2, inserirvi un nuovo parametro, quindi impostare param2 in una posizione e param1 con l’altra. Esempio:

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Convalida del parametro at_property nella richiesta di recupero preventivo

A questo punto, eseguite l&#39;emulatore e utilizzate Logcat per verificare che la proprietà at_property sia visualizzata nella richiesta di preacquisizione e nella risposta per entrambe le posizioni:
![Convalida del parametro at_property](assets/parameters_at_property_validation.jpg)

## Aggiunta di parametri personalizzati alla richiesta Live Location

La richiesta di posizione dal vivo (wetravel_context_dest) è stata aggiunta nella lezione precedente in modo da poter visualizzare una promozione rilevante nella schermata di conferma finale del processo di prenotazione. Vorremmo personalizzare la promozione in base alla destinazione dell&#39;utente e per farlo aggiungeremo questo parametro alla richiesta. Aggiungeremo anche un parametro per l&#39;origine trop e per il valore at_property.

Aggiungete i seguenti parametri alla funzione targetLoadRequest() nel controller GrazieYouActivity:
![Aggiungere parametri alla richiesta](assets/parameters_live_location.jpg)di posizione in diretta Questo è il codice aggiornato per la funzione targetLoadRequest() (aggiornare il testo segnaposto &quot;aggiungi qui il valore at_property&quot;!):

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Map<String, Object> locationParams = new HashMap<>();
    locationParams.put("at_property","add your at_property value here");
    locationParams.put("locationSrc", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.departure,"")));
    locationParams.put("locationDest", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.destination,"")));

    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, locationParams, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
        try {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    AppDialogs.dialogLoaderHide();
                    filterRecommendationBasedOnOffer(recommandations, response);
                    recommandationbAdapter.notifyDataSetChanged();
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
        }
    });
    Target.clearPrefetchCache();
}
```

### Convalida dei parametri personalizzati nella richiesta Live Location

Eseguire l&#39;emulatore e aprire Logcat. Filtrate uno dei parametri per verificare che la richiesta contenga i parametri necessari:
![Convalida dei parametri personalizzati nella richiesta Live Location](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>Richieste e parametri di conferma ordine: Anche se non utilizzati in questo progetto demo, i dettagli dell&#39;ordine vengono generalmente acquisiti in un&#39;implementazione reale, in modo da [!DNL Target] poter utilizzare i dettagli dell&#39;ordine come metriche/dimensioni. Per istruzioni su come [implementare la richiesta di conferma dell&#39;ordine e i relativi parametri](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html), consultate la documentazione.

>[!NOTE]
>
> Analytics per Target (A4T): Adobe  Analytics può essere configurato come origine di reporting per [!DNL Target]. Questo consente di visualizzare tutte le metriche/dimensioni raccolte dall’SDK Target in Adobe  Analytics. Per ulteriori dettagli, consultate Panoramica [](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) A4T.

Bel lavoro! Ora che i parametri sono impostati, siamo pronti a usare questi parametri per creare audience e offerte in  Adobe Target.

**[NEXT: &quot;Crea pubblico e offerte&quot; >](create-audiences-and-offers.md)**
