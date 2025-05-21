---
title: Aggiungere parametri alle richieste
description: In questa lezione aggiungeremo Adobi di metriche del ciclo di vita e parametri personalizzati alle richieste Target aggiunte nella lezione precedente. Queste metriche e parametri verranno utilizzati per creare tipi di pubblico personalizzati più avanti nell’esercitazione.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 0250e55f-a233-4060-84e1-86d1f88a6106
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Aggiungere parametri alle richieste

In questa lezione verranno aggiunti Adobi di metriche del ciclo di vita e parametri personalizzati alle richieste [!DNL Target] aggiunte nella lezione precedente. Queste metriche e parametri verranno utilizzati per creare tipi di pubblico personalizzati più avanti nell’esercitazione.

## Finalità di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Aggiungere l’Adobe di metriche del ciclo di vita mobile
* Aggiungere parametri a una richiesta di preacquisizione
* Aggiungere parametri a una posizione live
* Convalidare i parametri per entrambe le richieste

## Aggiungere i parametri del ciclo di vita

Abilitiamo [Adobe mobile lifecycle metrics](https://experienceleague.adobe.com/docs/mobile-services/android/metrics.html?lang=it). Questo aggiungerà parametri alle richieste di posizione contenenti informazioni dettagliate sul dispositivo dell’utente e sul coinvolgimento con l’app. Nella prossima lezione verranno creati dei tipi di pubblico utilizzando i dati forniti dalla richiesta del ciclo di vita.

Per abilitare le metriche del ciclo di vita, aprire nuovamente il controller HomeActivity e aggiungere `Config.collectLifecycleData(this);` alla funzione onResume():

![Richiesta ciclo di vita](assets/lifecycle_code.jpg)

### Convalidare i parametri del ciclo di vita per la richiesta di preacquisizione

Esegui l’emulatore e utilizza Logcat per convalidare i parametri del ciclo di vita. Filtra &quot;preacquisizione&quot; per trovare la risposta di preacquisizione e cercare i nuovi parametri:
![Convalida ciclo di vita](assets/lifecycle_validation.jpg)

Anche se abbiamo aggiunto solo `Config.collectLifecycleData()` al controller HomeActivity, le metriche del ciclo di vita inviate con la richiesta Target dovrebbero essere visualizzate anche nella schermata Grazie.

## Aggiungi il parametro at_property alla richiesta di preacquisizione

Le proprietà di Adobe Target sono definite nell&#39;interfaccia [!DNL Target] e vengono utilizzate per stabilire i limiti per la personalizzazione di app e siti Web. Il parametro at_property identifica la proprietà specifica in cui accedere e mantenere le offerte e le attività. Aggiungeremo una proprietà alle richieste di preacquisizione e di posizione live.

>[!NOTE]
>
>A seconda della licenza, è possibile che le opzioni Proprietà dell&#39;interfaccia [!DNL Target] non siano visualizzate. Se non disponi di queste opzioni o se non utilizzi le Proprietà nella tua azienda, passa alla sezione successiva di questa lezione.

Puoi recuperare il valore at_property nell&#39;interfaccia [!DNL Target] in [!UICONTROL Setup] > [!UICONTROL Properties].  Passa il puntatore del mouse sulla proprietà, seleziona l&#39;icona dello snippet di codice e copia il valore `at_property`:

![Copia at_property](assets/at_property_interface.jpg)

Aggiungilo come parametro per ogni posizione nella richiesta di preacquisizione, come segue:
![Aggiungi parametro at_property](assets/params_at_property.jpg)
Ecco il codice aggiornato per la funzione `targetPrefetchContent()` (assicurati di aggiornare il testo del segnaposto _[!UICONTROL your at_property value goes here]_):

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

### Nota sui parametri

Per i progetti futuri, potrebbe essere utile implementare parametri aggiuntivi. Il metodo `createTargetPrefetchObject()` consente tre tipi di parametri: `locationParams`, `orderParams` e `productParams`. Consulta la documentazione per [ulteriori dettagli sull&#39;aggiunta di questi parametri alla richiesta di preacquisizione](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=it).

Inoltre, è possibile aggiungere parametri di posizione diversi a ciascuna posizione nella richiesta di preacquisizione. Ad esempio, puoi creare un&#39;altra mappa denominata param2, inserirvi un nuovo parametro, quindi impostare param2 in una posizione e param1 con l&#39;altra posizione. Ecco un esempio:

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Convalidare il parametro at_property nella richiesta di preacquisizione

Ora esegui l’emulatore e utilizza Logcat per verificare che at_property sia visualizzato nella richiesta e nella risposta di preacquisizione per entrambe le posizioni:
![Convalida il parametro at_property](assets/parameters_at_property_validation.jpg)

## Aggiungere parametri personalizzati alla richiesta di posizione live

La richiesta di posizione live (wetravel_context_dest) è stata aggiunta nella lezione precedente in modo da poter visualizzare una promozione rilevante nella schermata di conferma finale del processo di prenotazione. Vorremmo personalizzare la promozione in base alla destinazione dell&#39;utente, aggiungendola come parametro alla richiesta. Aggiungeremo anche un parametro per l’origine della trappola e il valore at_property.

Aggiungere i seguenti parametri alla funzione targetLoadRequest() nel controller ThankYouActivity:
![Aggiungi parametri alla richiesta di posizione live](assets/parameters_live_location.jpg)
Ecco il codice aggiornato per la funzione targetLoadRequest() (assicurati di aggiornare il testo del segnaposto &quot;aggiungi qui il valore at_property&quot; ):

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

### Convalidare i parametri personalizzati nella richiesta di posizione live

Esegui l’emulatore e apri Logcat. Filtra uno dei parametri per verificare che la richiesta contenga i parametri necessari:
![Convalida i parametri personalizzati nella richiesta di posizione live](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>Richieste e parametri di conferma ordine: anche se non vengono utilizzati in questo progetto demo, i dettagli dell&#39;ordine vengono generalmente acquisiti in un&#39;implementazione reale, quindi [!DNL Target] può utilizzare i dettagli dell&#39;ordine come metriche/dimensioni. Fare riferimento alla documentazione per istruzioni su come [implementare la richiesta di conferma dell&#39;ordine e i parametri](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-target-methods.html?lang=it).

>[!NOTE]
>
>Analytics for Target (A4T): Adobe Analytics può essere configurato come origine per la generazione di rapporti per [!DNL Target]. Questo consente di visualizzare in Adobe Analytics tutte le metriche/dimensioni raccolte dall’SDK di Target. Per ulteriori dettagli, consulta la [Panoramica di A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=it).

Ottimo lavoro. Ora che i parametri sono operativi, possiamo utilizzarli per creare tipi di pubblico e offerte in Adobe Target.

**[AVANTI: &quot;Crea tipi di pubblico e offerte&quot; >](create-audiences-and-offers.md)**
