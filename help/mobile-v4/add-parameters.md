---
title: Aggiungere parametri alle richieste
description: In questa lezione aggiungeremo metriche del ciclo di vita di Adobe e parametri personalizzati alle richieste Target aggiunte nella lezione precedente. Queste metriche e questi parametri verranno utilizzati per creare tipi di pubblico personalizzati più avanti nell’esercitazione.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 0250e55f-a233-4060-84e1-86d1f88a6106
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Aggiungere parametri alle richieste

In questa lezione aggiungeremo metriche del ciclo di vita di Adobe e parametri personalizzati alle richieste [!DNL Target] aggiunte nella lezione precedente. Queste metriche e questi parametri verranno utilizzati per creare tipi di pubblico personalizzati più avanti nell’esercitazione.

## Obiettivi di apprendimento

Al termine di questa lezione, potrai:

* Aggiungere le metriche del ciclo di vita di Adobe per dispositivi mobili
* Aggiungere parametri a una richiesta di preacquisizione
* Aggiungi parametri a una posizione live
* Convalida i parametri per entrambe le richieste

## Aggiungere i parametri del ciclo di vita

Abilita le [metriche del ciclo di vita mobile di Adobe](https://experienceleague.adobe.com/docs/mobile-services/android/metrics.html?lang=en). Questo aggiungerà parametri alle richieste di posizione contenenti informazioni dettagliate sul dispositivo dell’utente e sul coinvolgimento con l’app. Nella prossima lezione creeremo dei tipi di pubblico utilizzando i dati forniti dalla richiesta del ciclo di vita.

Per abilitare le metriche del ciclo di vita, apri nuovamente il controller HomeActivity e aggiungi `Config.collectLifecycleData(this);` alla funzione onResume() :

![Richiesta del ciclo di vita](assets/lifecycle_code.jpg)

### Convalida i parametri del ciclo di vita per la richiesta di preacquisizione

Esegui l’emulatore e utilizza Logcat per convalidare i parametri del ciclo di vita. Filtra per &quot;preacquisizione&quot; per trovare la risposta di preacquisizione e cercare i nuovi parametri:
![Convalida del ciclo di vita](assets/lifecycle_validation.jpg)

Anche se abbiamo aggiunto solo `Config.collectLifecycleData()` al controller HomeActivity, dovresti vedere anche le metriche del ciclo di vita inviate con la richiesta Target nella schermata di ringraziamento.

## Aggiungi il parametro at_property alla richiesta di preacquisizione

Le proprietà di Adobe Target sono definite nell&#39;interfaccia [!DNL Target] e vengono utilizzate per stabilire i limiti per la personalizzazione di app e siti web. Il parametro at_property identifica la proprietà specifica in cui è possibile accedere e mantenere le offerte e le attività. Verrà aggiunta una proprietà alle richieste di preacquisizione e di posizione attiva.

>[!NOTE]
>
>È possibile visualizzare o meno le opzioni Proprietà nell&#39;interfaccia [!DNL Target], a seconda della licenza. Se non disponi di queste opzioni o se non utilizzi Proprietà nella tua azienda, passa alla sezione successiva di questa lezione.

È possibile recuperare il valore at_property nell&#39;interfaccia [!DNL Target] in [!UICONTROL Configurazione] > [!UICONTROL Proprietà].  Passa il puntatore del mouse sulla proprietà, seleziona l’icona del frammento di codice e copia il valore `at_property` :

![Copia at_property](assets/at_property_interface.jpg)

Aggiungilo come parametro per ogni posizione nella richiesta di preacquisizione come segue:
![Aggiungi parametro at_property](assets/params_at_property.jpg)
Ecco il codice aggiornato per la funzione `targetPrefetchContent()` (assicurati di aggiornare il _[!UICONTROL valore at_property qui]_ testo segnaposto!):

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

Per i progetti futuri, potrebbe essere utile implementare parametri aggiuntivi. Il metodo `createTargetPrefetchObject()` consente tre tipi di parametri: `locationParams`, `orderParams` e `productParams`. Consulta la documentazione per [ulteriori dettagli sull&#39;aggiunta di questi parametri alla richiesta di preacquisizione](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=en).

Inoltre, puoi aggiungere diversi parametri di posizione a ogni posizione nella richiesta di preacquisizione. Ad esempio, puoi creare un&#39;altra mappa chiamata param2, inserirvi un nuovo parametro, quindi impostare param2 in una posizione e param1 con l&#39;altra posizione. Ecco un esempio:

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Convalida il parametro at_property nella richiesta di preacquisizione

Ora esegui l’emulatore e utilizza Logcat per verificare che la proprietà at_property sia visualizzata nella richiesta di preacquisizione e nella risposta per entrambe le posizioni:
![Convalida il parametro at_property](assets/parameters_at_property_validation.jpg)

## Aggiungi parametri personalizzati alla richiesta Live Location

La richiesta di posizione live (wetravel_context_dest) è stata aggiunta nella lezione precedente in modo da poter visualizzare una promozione pertinente nella schermata di conferma finale del processo di prenotazione. Vorremmo personalizzare la promozione in base alla destinazione dell’utente e a questo scopo aggiungeremo la promozione come parametro alla richiesta. Aggiungeremo anche un parametro per l&#39;origine trop e il valore at_property.

Aggiungi i seguenti parametri alla funzione targetLoadRequest() nel controller GrazieYouActivity:
![Aggiungi parametri alla Live Location Request](assets/parameters_live_location.jpg)
Ecco il codice aggiornato per la funzione targetLoadRequest() (assicurati di aggiornare il testo segnaposto &quot;aggiungi il valore at_property qui&quot;!):

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

### Convalidare i parametri personalizzati nella richiesta Live Location

Esegui l&#39;emulatore e apri Logcat. Filtra per uno dei parametri per verificare che la richiesta contenga i parametri necessari:
![Convalida i parametri personalizzati nella Live Location Request](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>Richieste e parametri di conferma dell’ordine: Sebbene non sia utilizzato in questo progetto demo, i dettagli dell’ordine vengono solitamente acquisiti in un’implementazione reale, in modo che [!DNL Target] possa utilizzare i dettagli dell’ordine come metriche/dimensioni. Fai riferimento alla documentazione per istruzioni su come [implementare la richiesta di conferma dell&#39;ordine e i parametri](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-target-methods.html?lang=en).

>[!NOTE]
>
>Analytics for Target (A4T): Adobe Analytics può essere configurato come origine per la generazione di rapporti per [!DNL Target]. Questo consente di visualizzare in Adobe Analytics tutte le metriche/dimensioni raccolte dall’SDK di Target. Per ulteriori informazioni, consulta la sezione [Panoramica di A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=en) .

Ottimo lavoro! Ora che i parametri sono impostati, siamo pronti per utilizzare questi parametri per creare audience e offerte in Adobe Target.

**[SUCCESSIVO : &quot;Crea pubblico e offerte&quot; >](create-audiences-and-offers.md)**
