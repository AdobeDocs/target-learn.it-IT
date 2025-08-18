---
title: Ottimizzare l’implementazione di Adobe Target
description: Panoramica dell’implementazione e della struttura di Adobe Target. Scopri come comprendere e controllare la configurazione della tua organizzazione. Scopri le tecniche di risoluzione dei problemi più comuni e i suggerimenti per la creazione di un archivio delle conoscenze per il tuo team.
solution: Target
feature: Overview
role: Leader, User
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# Ottimizzare l’implementazione di Adobe Target

Se hai poca esperienza con la tua organizzazione e desideri acquisire familiarità con ciò che è in atto da una procedura di test e ottimizzazione, questo articolo ti aiuta a iniziare. Inizieremo con una panoramica dell’implementazione e della struttura di Adobe Target. Scoprirai come comprendere e controllare la configurazione della tua organizzazione. Infine, verranno illustrate le tecniche più comuni per la risoluzione dei problemi e i suggerimenti per la creazione di un archivio delle conoscenze per il team.

Adobe Target è uno strumento che consente di testare e indirizzare contenuti univoci a visitatori diversi. Per una panoramica delle funzionalità disponibili, [visita questa guida](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=it).

## Implementazione e struttura del target

Prima di approfondire il processo di implementazione di Adobe Target o la sua struttura, è utile comprendere alcune nozioni di base sul software.

Adobe Target è uno strumento che consente di testare e indirizzare contenuti univoci a visitatori diversi senza modificare il codice nativo del sito web. Target modifica temporaneamente l’esperienza dell’utente finale e tiene traccia del comportamento degli utenti dopo aver visto la modifica. Target consente inoltre di modificare l’esperienza per gli utenti finali in base alle informazioni sul profilo o alle azioni precedenti.

Esistono tre tipi di attività fondamentali di Target:

1. Test A/B
2. Test multivariato (MVT)
3. Test dell’esperienza

**Il test A/B** confronta due o più esperienze per vedere quale migliora meglio le conversioni durante un periodo di test predefinito. Il test A/B è un esperimento altamente controllato con misurazioni del traffico, suddiviso in percentuali anziché da una regola, che consente di:

* per analizzare i dati di prova.
* per ottenere informazioni sul pubblico.
* per determinare quale esperienza funziona meglio.

**Il test multivariato** (MVT) confronta le combinazioni di offerte tra gli elementi di una pagina per vedere quale combinazione funziona meglio per un pubblico specifico. Questo test identifica anche l’elemento della pagina che migliora le conversioni nel modo migliore durante un periodo di test pre-specificato. MVT fornisce:

* Un modo per visualizzare più offerte in più elementi.
* Un metodo per testare l’esperienza univoca risultante rispetto a un obiettivo specifico.
* Insight su quali elementi hanno il maggiore impatto negativo o positivo sulle interazioni dei visitatori.

**Experience testing** (Targeting esperienza) fornisce contenuti a un pubblico specifico in base a una serie di regole e criteri definiti dall&#39;addetto al marketing. Questo metodo permette di indirizzare contenuti specifici a un pubblico specifico in base a una serie di regole di allocazione definite.

Come funziona Target?

Ecco un esempio di alto livello del funzionamento di Target:

1. Un visitatore richiede una pagina dal server e la visualizza nel browser.
1. Un cookie di prima parte viene impostato nel browser del visitatore per memorizzare il comportamento.
1. La pagina chiama quindi Adobe Target.
1. Il contenuto viene visualizzato in base alle regole dell’attività dell’utente.
1. Adobe Target acquisisce metriche specifiche come definito nella configurazione dell’attività per misurare l’impatto delle esperienze di test.

Target è basato su una &quot;mbox globale&quot; che consente di influire su qualsiasi elemento della pagina. Questa funzione viene implementata al caricamento della pagina come collegamento hardcoded al file at.js oppure viene distribuita utilizzando un gestore di tag come Adobe Launch.

## Comprendere l’implementazione corrente

Per comprendere l’implementazione corrente, Adobe consiglia di rivedere l’implementazione dell’interfaccia utente di Target insieme a quella di Tag Manager e Caricamento pagina.

**Per rivedere l&#39;interfaccia utente di [!DNL Target]:**

1. Inizia la tua recensione sull&#39;interfaccia utente [!DNL Target]:

   * Esaminare lo stack di tecnologia [!DNL Target]
   * Conferma le funzioni disponibili
   * Identificare la posizione in cui è attiva la distribuzione

1. Rivedi le attività per le best practice:

   * Rivedi campagne storiche per la maturità del programma

1. Disattiva vecchie attività:

   * Archivia e pulisci [!DNL Target] risorsa che non verrà più utilizzata

1. Rivedi i tipi di pubblico.

1. Esamina le definizioni dell’ambiente e i domini associati.

1. Esamina gli script di profilo per verificarne l’applicabilità

   * Tutti gli script di profilo vengono eseguiti su ogni chiamata di destinazione
   * Mantenere l’efficienza delle chiamate rimuovendo gli script non applicabili

Per rivedere il gestore tag e il caricamento della pagina:

1. In Gestione tag, conferma quanto segue:

   * Distribuzione del codice JavaScript [!DNL Target] previsto
   * La soluzione appropriata per nascondere i contenuti
   * Imposta le regole necessarie per popolare le chiamate [!DNL Target] con i parametri previsti

1. Conferma quanto segue durante il caricamento della pagina:

   * Numeri di versione corrispondenti per l&#39;URL della richiesta e l&#39;URL della richiesta [!DNL Target]
   * Valore ID cloud esperienza popolato (corpo del cloud)
   * Presentare i valori di integrazione previsti (Cloud Body)
   * Ha compilato [!DNL Target] parametri sulle pagine appropriate

## [!DNL Target] attività di audit

Per evitare di scorrere manualmente ogni pagina per controllare [!DNL Target] attività, utilizza Adobe Auditor per comprendere lo stato tecnico corrente dell&#39;implementazione. Adobe Auditor è basato su ObservePoint e può essere configurato per essere eseguito a livello manuale, per identificare problemi di implementazione di alto livello sul sito.

Adobe Auditor fornisce:

* Salute del sito elevata
* Chiamate rapide per problemi di implementazione

Adobe consiglia di eseguire audit manuali mensili per:

* Identificare le pagine senza tag
* Identificare le versioni incoerenti
* Trova versioni non aggiornate
* Fornire informazioni dettagliate che possono essere esportate

## Risoluzione dei problemi comuni

>[!NOTE]
>
>Adobe consiglia di installare Adobe Experience Platform Debugger.

Di seguito sono riportati alcuni suggerimenti generali per la risoluzione di problemi durante l’accesso all’esperienza:

### Cache e cookie**

* Cancellazione cache e cookie
* Presta attenzione quando utilizzi la modalità privata (ad esempio, la modalità privata in Firefox può bloccare [!DNL Target])

### Sei qualificato per l&#39;attività?

* Verifica di aver eseguito gli stessi passaggi utilizzati dal pubblico nell’attività
* Utilizza `mboxTrace` o i token di risposta per controllare i valori di profilo e segmento

### Suggerimenti generali per la risoluzione dei problemi durante la convalida visiva/funzionale

Se si trova nell&#39;esperienza [!DNL Target] e non si visualizza l&#39;esperienza visiva prevista:

Controlla la risposta di [!DNL Target]:

* Se il codice non viene eseguito:

1. Controllare le attività in conflitto
1. Contatta l’Assistenza clienti

* Se il codice viene eseguito:

1. Rielabora il codice in quello scenario

## Gestione di un archivio delle conoscenze

Un archivio delle conoscenze è una piattaforma online utilizzata per documentare e condividere le informazioni. L’archivio delle conoscenze contiene informazioni specifiche per l’implementazione e può contenere informazioni specifiche per il team.

Idealmente, l’archivio dovrebbe consentire la modifica e il salvataggio automatico all’interno della piattaforma. Una volta configurato inizialmente, è facile mantenerlo e tenerlo aggiornato. Il contenuto all’interno del Knowledge Repository viene curato in base ai ruoli utente.

I documenti tipici di un Archivio Knowledge Base includono:

* **Documento introduttivo**: documento utilizzato per spiegare chiaramente obiettivi, obiettivi, processi e struttura del programma
* **Archivio ideazione**: documento utilizzato per gestire e assegnare la priorità a potenziali idee non pronte per il processo di test
* **Roadmap del programma**: documento utilizzato per gestire tutti gli aspetti delle attività di test quando le idee sono pronte per avviare il processo di test
* **Documento piano di attività**: documento utilizzato per delineare le informazioni necessarie per generare e avviare le attività
* **Documento del piano di attività**: documento utilizzato per comunicare i risultati e i passaggi successivi consigliati alle parti interessate
* **Dashboard del programma**: documento utilizzato per monitorare le prestazioni del programma, la cadenza e i vantaggi in termini di ricavi nel tempo.

Per ulteriori informazioni, consulta il nostro [webinar](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) con Senior Consultant, Wilder Freed.

Ulteriori informazioni su strategia e leadership di pensiero nell&#39;hub [Customer Success](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html?lang=it).
