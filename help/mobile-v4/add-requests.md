---
title: Aggiungere richieste Adobe Target
description: Il SDK di Adobe Mobile Services (v4) fornisce metodi e funzionalità Adobe Target che consentono di personalizzare l’app con esperienze diverse per utenti diversi.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 88a5be3f-d61f-43e7-997a-574ef56122ed
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---

# Aggiungere richieste Adobe Target

Il SDK di Adobe Mobile Services (v4) fornisce metodi e funzionalità Adobe Target che consentono di personalizzare l’app con esperienze diverse per utenti diversi. In genere, l’app invia all’Adobe Target una o più richieste per recuperare il contenuto personalizzato e misurarne l’impatto.

In questa lezione, preparerai l&#39;app We.Travel per la personalizzazione implementando [!DNL Target] richieste.

## Prerequisiti

Assicurarsi di [scaricare e aggiornare l&#39;app di esempio](download-and-update-the-sample-app.md).

## Finalità di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Memorizza nella cache più offerte [!DNL Target] (ad esempio contenuto personalizzato) utilizzando una richiesta di preacquisizione batch
* Carica posizioni [!DNL Target] preacquisite
* Carica una posizione [!DNL Target] in tempo reale (non precaricata)
* Cancella posizioni preacquisite dalla cache
* Convalidare richieste preacquisite e in tempo reale

## Terminologia 

Di seguito sono riportati alcuni termini chiave di Target che utilizzeremo nel resto di questa esercitazione.

* **Richiesta:** una richiesta di rete ai server Adobe Target
* **Offerta:** uno snippet di codice o altro contenuto basato su testo, definito nell&#39;interfaccia utente di [!DNL Target] (o con API), che viene distribuito nella risposta. Di solito JSON quando [!DNL Target] viene utilizzato nelle app native per dispositivi mobili.
* **Posizione:** un nome definito dall&#39;utente assegnato a una richiesta, utilizzato nell&#39;interfaccia [!DNL Target] per associare le offerte a richieste specifiche
* **Richiesta batch:** una singola richiesta che include più posizioni
* **Richiesta di preacquisizione:** una singola richiesta che recupera le offerte e le memorizza in cache per utilizzarle in futuro nell&#39;app
* **Richiesta di preacquisizione batch:** una singola richiesta che preacquisisce offerte per più posizioni
* **Pubblico:** un gruppo di visitatori definito nell&#39;interfaccia [!DNL Target] o condiviso con [!DNL Target] da altre applicazioni Adobe (ad esempio &quot;Visitatori iPhone X&quot;, &quot;Visitatori in California&quot;, &quot;Prima app aperta&quot;)
* **Attività:** un costrutto [!DNL Target], definito nell&#39;interfaccia utente [!DNL Target] (o con API) che collega posizioni, offerte e tipi di pubblico per creare un&#39;esperienza personalizzata

## Aggiungi una richiesta di preacquisizione batch

La prima richiesta che implementeremo in We.Travel è una richiesta di preacquisizione batch con due posizioni [!DNL Target] nella schermata iniziale. In una lezione successiva, configureremo le offerte per queste posizioni che visualizzano messaggi per aiutare i nuovi utenti nel processo di prenotazione.

Una richiesta di preacquisizione recupera il contenuto di [!DNL Target] il meno possibile memorizzando nella cache la risposta del server Adobe Target (offerta). Una richiesta di preacquisizione batch recupera e memorizza nella cache più offerte, ciascuna associata a una posizione diversa. Tutte le posizioni preacquisite vengono memorizzate nella cache del dispositivo per un utilizzo futuro nella sessione utente. Preacquisendo più posizioni nella schermata iniziale, possiamo recuperare le offerte da utilizzare in un secondo momento mentre il visitatore naviga attraverso l’app. Per ulteriori dettagli sui metodi di preacquisizione, consulta la [documentazione di preacquisizione](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=en).

### Aggiungi la richiesta di preacquisizione batch

Aggiorniamo il controller HomeActivity (il codice sorgente della schermata Home), che si trova in app > main > java > com.wetravel > Controller. Aggiungeremo i due blocchi di codice mostrati in rosso:

Inizieremo con il controller HomeActivity (il codice sorgente della schermata Home), che si trova in app > main > java > com.wetravel > Controller.

Aggiungeremo i due blocchi di codice mostrati in rosso:

![Codice di preacquisizione HomeActivity](assets/homeactivity.jpg)

Scorri verso il basso fino alla fine del codice di HomeActivity e aggiungi il codice fornito di seguito dopo la funzione `setHeader()` e *sostituendo* la funzione `onResume()` corrente:

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

È probabile che l&#39;IDE ti avviserà che le classi [!DNL Target] non sono state importate nel file. Assicurarsi di importare le classi [!DNL Target] nella parte superiore del controller HomeActivity, come illustrato di seguito in rosso:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importa le classi di destinazione](assets/import.jpg)

È probabile che vengano visualizzati errori anche per &quot;impossibile trovare la variabile simbolo wetravel_engagement_home&quot; e &quot;impossibile trovare la variabile simbolo wetravel_eng_search&quot;. Aggiungi questi al file `Constant.java` (in app > src > main > java > com > wetravel > Utils):

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Aggiungere i nomi dei percorsi al file Constant.java](assets/constants.jpg)

### Spiegazione del codice di richiesta di preacquisizione batch

| Codice | Descrizione |
|--- |--- |
| `targetPrefetchContent()` | Funzione definita dall&#39;utente (non inclusa in SDK) che utilizza i metodi [!DNL Target] per recuperare e memorizzare nella cache due posizioni [!DNL Target]. |
| `prefetchContent()` | Il metodo SDK [!DNL Target] che invia la richiesta di preacquisizione |
| `Constant.wetravel_engage_home` | Nome posizione [!DNL Target] preacquisito che visualizzerà il contenuto dell&#39;offerta nella schermata iniziale |
| `Constant.wetravel_engage_search` | Nome percorso [!DNL Target] preacquisito che visualizzerà il contenuto dell&#39;offerta nella schermata Risultati ricerca. Poiché si tratta di una seconda posizione nella preacquisizione, questa richiesta di preacquisizione è denominata &quot;richiesta batch di preacquisizione&quot;. |
| setUp() | Funzione definita dall&#39;utente che esegue il rendering della schermata iniziale dell&#39;app dopo il recupero delle offerte [!DNL Target] |

### Informazioni su asincrono e sincrono

Con il codice appena implementato, la richiesta di preacquisizione viene effettuata come chiamata sincrona di blocco, appena prima del rendering della schermata iniziale. Quando abbiamo incollato il nuovo codice nel controller HomeActivity, l&#39;esecuzione della funzione `setUp()` è stata spostata dalla funzione `onResume()` a dopo la richiesta Target. Questo può essere utile negli scenari in cui desideri personalizzare il contenuto quando l’app si apre per la prima volta, perché assicura che il contenuto personalizzato dai server di Target sia stato restituito (o scaduto) prima del rendering della prima schermata. Per consentire il caricamento asincrono delle richieste (in background), è sufficiente chiamare `setUp()` nella funzione `onCreate()`.

### Convalidare la richiesta di preacquisizione batch

Rigenera l’app e apri l’emulatore Android. Le schermate seguenti utilizzano Pixel 2 su Android Q versione 9+, API livello 29. La risposta di preacquisizione deve riportare il testo &quot;risposta di preacquisizione ricevuta&quot;:

Quando viene eseguito il rendering della schermata iniziale, la richiesta di preacquisizione deve essere caricata. Con Logcat, filtra per [!DNL "Target"] per visualizzare la richiesta e la risposta:

![Convalida le richieste nella schermata iniziale](assets/prefetch_validation.jpg)

Se la risposta non viene visualizzata correttamente, verificare le impostazioni nel file `ADBMobileConfig.json` e la sintassi del codice nel file HomeActivity.

Due posizioni sono ora memorizzate nella cache del dispositivo. I nomi delle posizioni verranno presto caricati in modo lento nell&#39;interfaccia [!DNL Target], dove possono essere selezionati in vari menu a discesa quando vengono utilizzati in un&#39;attività.

### Aggiungi richieste di caricamento per ogni posizione memorizzata nella cache

Ora che le posizioni sono preacquisite e le loro risposte sono memorizzate nella cache del dispositivo, aggiungiamo il metodo `Target.loadRequest()` che recupera il contenuto dell&#39;offerta dalla cache in modo che tu possa utilizzarlo per aggiornare l&#39;applicazione. Verrà aggiunto un nuovo metodo personalizzato denominato `engageMessage()` che verrà eseguito con la richiesta di preacquisizione. `engageMessage()` chiamerà `Target.loadRequest()`. `engageMessage()` viene eseguito prima di `setUp()` per assicurarsi che la richiesta di caricamento venga chiamata prima della configurazione dello schermo.

Innanzitutto, aggiungi la chiamata e il metodo `engageMessage()` per la posizione wetravel_eng_home nell&#39;attività Home:

![Aggiungi prima richiesta di caricamento](assets/wetravel_engage_home_loadRequest.jpg)

Ecco il codice aggiornato:

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
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

Aggiungere ora la chiamata e il metodo `engageMessage()` per la posizione wetravel_eng_search in SearchBusActivity. Si noti che la chiamata `engageMessage()` è impostata nel metodo `onResume()` prima della chiamata a `setUpSearch()`, quindi viene eseguita prima della configurazione della schermata:

![Aggiungi seconda richiesta di caricamento](assets/wetravel_engage_search_loadRequest.jpg)

Ecco il codice aggiornato:

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

Poiché hai appena aggiunto i metodi Target a SearchBusActivity, assicurati di importare le classi [!DNL Target]:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Aggiungere una richiesta in tempo reale

La prossima richiesta che aggiungeremo all’app sarà una richiesta in tempo reale nella schermata di ringraziamento. Con &quot;tempo reale&quot; si intende che la richiesta verrà effettuata e la risposta verrà applicata immediatamente (non memorizzata nella cache per un momento successivo). In una lezione successiva, genereremo un’esperienza utilizzando questa richiesta, personalizzata in base alla destinazione del viaggio dell’utente.

Aggiungiamo quindi una richiesta in tempo reale nella schermata di ringraziamento. Nel file ThankYouActivity, le modifiche visualizzate sono in rosso:
![Aggiungi una posizione in tempo reale nella schermata di ringraziamento](assets/thankyou.jpg)

Scorri fino alla fine del file ThankYouActivity. Commentare le tre righe della funzione `getRecommandations()` e aggiungere la chiamata della funzione `targetLoadRequest()`:

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

Aggiungi questa riga di codice alla funzione `getRecommandations()`:

```java
targetLoadRequest(recommandation.recommandations);
```

Ora è necessario definire la funzione `targetLoadRequest()`:
![Aggiungi una posizione in tempo reale nella schermata di ringraziamento](assets/thankyou2.jpg)

Aggiungi questo blocco di codice dopo la funzione `filterRecommendationBasedOnOffer()`:

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
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
}
```

Poiché hai appena aggiunto i metodi Target all’attività ThankYouActivity, assicurati di importare le classi Target:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### spiegazione del codice targetLoadRequest()

| Codice | Descrizione |
|--- |--- |
| `targetLoadRequest()` | Funzione definita dall&#39;utente (non inclusa in SDK) che attiva `Target.loadRequest()` e carica e visualizza la posizione wetravel_context_dest |
| `Target.loadRequest()` | Il metodo SDK che invia la richiesta al server di Target |
| Constant.wetravel_context_dest | Il nome della posizione assegnato alla richiesta che utilizzeremo in seguito quando verrà generata l&#39;attività nell&#39;interfaccia [!DNL Target] |
| `filterRecommendationBasedOnOffer()` | Funzione definita dall’utente nell’app che prende l’offerta della posizione dalla risposta di Target e decide come l’app deve cambiare in base al contenuto dell’offerta |
| `recommandations.addAll()` | Funzione definita dall&#39;utente nell&#39;app che veniva eseguita per impostazione predefinita al caricamento della schermata Grazie, ma ora viene eseguita dopo che la risposta di Target è stata ricevuta e analizzata da `filterRecommendationBasedOnOffer()` |

Questo è stato un aggiornamento più sofisticato che abbiamo apportato all’app, poi con la richiesta che abbiamo aggiunto alla schermata iniziale, quindi proviamo a rivedere quello che abbiamo fatto:

1. Abbiamo interrotto il comportamento precedente dell’app di mostrare tre promozioni predefinite, commentando le righe di codice
1. Abbiamo chiesto all’app di eseguire una nuova funzione, chiamata arbitrariamente targetLoadRequest
1. È stata definita la funzione `targetLoadRequest` per effettuare una richiesta a Target utilizzando il metodo Target.loadRequest ed eseguire immediatamente la funzione `filterRecommendationBasedOnOffer()` quando viene ricevuta la risposta all&#39;offerta [!DNL Target]
1. La funzione `filterRecommendationBasedOnOffer()` interpreta la risposta e decide quali promozioni applicare allo schermo

Si tratta di un modello di utilizzo molto comune quando si utilizza [!DNL Target] nelle app per dispositivi mobili.  È entrambi molto potente, in quanto puoi personalizzare quasi qualsiasi aspetto della tua app mobile. Richiede anche il coordinamento tra il codice dell&#39;app e le offerte che definiremo più avanti nell&#39;interfaccia [!DNL Target]. A causa di questo coordinamento, per alcuni casi di utilizzo di personalizzazione potrebbe essere necessario aggiornare l’app nell’app store per avviare l’attività.

### Convalidare la richiesta in tempo reale

Apri l’emulatore Android e segui tutti i passaggi per prenotare un viaggio: Home > Risultati ricerca bus > Selezione posti, Opzioni di pagamento (funziona qualsiasi opzione di pagamento con dati vuoti).

Nella schermata di ringraziamento finale, guarda Logcat per la risposta. La risposta deve contenere il testo &quot;Il contenuto predefinito è stato restituito per &quot;wetravel_context_dest&quot;:

![Aggiungi una posizione in tempo reale nella schermata di ringraziamento](assets/thankyou_validation.jpg)

## Cancellazione delle posizioni di prelettura dalla cache

In alcune situazioni, le posizioni preacquisite devono essere cancellate durante una sessione. Ad esempio, quando si verifica una prenotazione, ha senso cancellare le posizioni memorizzate in cache, poiché l’utente è ora &quot;coinvolto&quot; e comprende il processo di prenotazione. Se prenotano un altro viaggio durante la sessione, non avranno bisogno delle posizioni originali nella schermata iniziale e nella schermata dei risultati di ricerca per guidare la prenotazione. Avrebbe più senso cancellare le posizioni dalla cache e preacquisire nuove offerte per una seconda prenotazione scontata o per un altro scenario pertinente. Puoi aggiungere la logica alla schermata iniziale e alla schermata dei risultati della ricerca per preacquisire nuove posizioni se durante la sessione è stata effettuata una prenotazione.

Per questo esempio, cancelleremo solo le posizioni preacquisite per la sessione quando avviene una prenotazione. Questa operazione viene eseguita chiamando la funzione `Target.clearPrefetchCache()`. Impostare la funzione all&#39;interno della funzione `targetLoadRequest()` come illustrato di seguito:

```java
Target.clearPrefetchCache()
```

![Cancella percorsi preacquisiti dalla cache](assets/clearPrefetch.jpg)

Congratulazioni! L’app ora dispone del framework per la personalizzazione. Nella prossima lezione, miglioreremo le nostre funzionalità di personalizzazione aggiungendo parametri a queste posizioni.

**[AVANTI: &quot;Aggiungi parametri&quot; >](add-parameters.md)**
