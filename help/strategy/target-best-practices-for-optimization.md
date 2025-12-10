---
title: Best practice per l’ottimizzazione
description: Scopri le sei nozioni di base di Adobe sull’ottimizzazione e come applicarle.
solution: Target
role: Leader, Developer, Admin
feature: Overview
level: Beginner
exl-id: dd29faea-bb67-4128-b261-fa407ba7158c
source-git-commit: ac4fad8a7fb77852b1bd27b9b6d49e55f8aa975a
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%

---

# Best practice per l’ottimizzazione con Adobe Target

Scopri le sei nozioni di base di Adobe sull’ottimizzazione e come applicarle.

Quando si tratta di creare una forte presenza digitale, il team dovrà affrontare una serie di sfide. Oltre al compito di coinvolgere centinaia, persino migliaia di clienti, i clienti mostrano una varietà di comportamenti e preferenze unici che cambieranno nel tempo e spetta non solo a te tenere il passo con tali cambiamenti, ma anche anticiparli ed eseguire le tue strategie in modo efficiente e preciso. Si tratta di una corsa contro la concorrenza in una maratona perpetua di contenuti, che richiede iterazione costante e tecnologia all&#39;avanguardia.

Una soluzione a questa sfida multifunzionale è l’ottimizzazione con Adobe Target, che assicura una presenza digitale in evoluzione pertinente, preziosa e priva di attrito. L&#39;architettura tecnica e i canali di distribuzione di [!DNL Target] varieranno notevolmente da un cliente all&#39;altro, tuttavia abbiamo stilato un elenco di best practice e strategie di ottimizzazione che ogni team può utilizzare per sfruttare appieno le funzionalità di questo potente strumento.

## Informazioni sull’ottimizzazione

L’ottimizzazione è definita come &quot;l’azione di fare l’uso migliore o più efficace di una situazione o di una risorsa&quot;. È il modo più efficiente per essere certi di disporre di dati qualitativi che dimostrino che le modifiche che stai apportando sono importanti. Per ottimizzare al meglio, devi essere in grado di misurare l’impatto e il valore dei tuoi sforzi. In caso contrario, le modifiche apportate comporteranno costi più elevati e un guadagno minimo. Per raggiungere questo obiettivo in modo efficace ed efficiente, devi iniziare con una pianificazione strategica. Senza includere un piano strategico nella tua ottimizzazione, non faresti altro che indovinare.

### Sei nozioni di base sull’ottimizzazione

1. **Strategizza**: identifica le opportunità per le attività in linea con gli obiettivi aziendali e basate sui dati.
1. **Assegna priorità**: classifica e pianifica le attività in base all&#39;allineamento aziendale, al livello di impegno e all&#39;impatto potenziale.
1. **Progettazione**: crea visualizzazioni finalizzate delle esperienze di attività e sviluppa piani di attività con criteri dettagliati.
1. **Genera ed esegui**: attività di sviluppo che includono configurazione di [!DNL Target], sviluppo del codice e test di controllo qualità.
1. **Analizza**: avvia l&#39;attività [!DNL Target] per la produzione e monitora le prestazioni per la durata dell&#39;attività.
1. **Azione e iterazione**: sviluppo di raccomandazioni in base alle prestazioni dell&#39;attività di test o personalizzazione.

Sapendo che il cambiamento è una costante, la nostra strategia di ottimizzazione dovrebbe essere un ciclo di esecuzione iterativo per soddisfare le esigenze in continua evoluzione dei tuoi clienti (vedi la figura 1 di seguito).

![Ottimizzazione e personalizzazione](assets/optimize-and-personalize.png)

_Figura 1 - Ciclo iterativo di ottimizzazione_

## Creazione di una strategia di ottimizzazione

Il processo di sviluppo di una strategia di ottimizzazione può essere suddiviso in: (1) Creare un piano di attività di test e (2) Comprendere le nozioni di base sull’ottimizzazione.

1: Il piano di attività del test deve essere documentato. In questo modo puoi ottenere uno standard minimo di qualità per quanto riguarda l’applicazione dell’attività di test. Il piano di attività del test deve includere:

* **Nome e descrizione:** Nome intuitivo dell&#39;attività e descrizione su cosa si concentra l&#39;esperimento. &quot;Come? Cosa? Quando? Dove? Perché?&quot;

* **Obiettivo:** Scopo dell&#39;attività e obiettivo di business allineato su cui è progettata per influire.

* **Ipotesi:** un&#39;ipotesi è una previsione creata prima dell&#39;esecuzione di un esperimento. Indica chiaramente cosa viene testato, cosa pensate che ne sarà del risultato e perché pensate che sia così. L’esecuzione dell’esperimento può dimostrare o confutare l’ipotesi.

Un’ipotesi completa si articola in tre parti:

* Se _variabile_
* Quindi _risultato_
* Perché _razionale_

* **Posizione:** URL, sezione pagina e tipo di dispositivo.
* **Metrica per obiettivo:** Come verrà misurato il successo?
* **Metriche secondarie:** altri importanti indicatori di prestazioni chiave (KPI, Key Performance Indicators) da valutare con lo scopo di comprendere ulteriormente l&#39;impatto e le iterazioni di pianificazione.
* **Pubblico attività:** Descrizione del filtro dell&#39;esposizione al test richiesto.
* **Tipi di pubblico per reportistica:** Elenco di descrizioni dei sottoinsiemi di visitatori da utilizzare per l&#39;analisi.
* **Experience Concepts:** trappole, esempi di wireframe e descrizioni.

**Nota generale:** è possibile testare qualsiasi elemento di una pagina web che possa promuovere il valore aziendale o fornire valore insight al comportamento del visitatore. Alcuni tipi comuni di attività di test includono:

* Testo titolo
* Testo contenuto
* Testo pulsante
* Layout di pagina
* Fotografia
* Colore pulsante
* Layout degli elementi
* Rimozione e aggiunta di elementi
* Ordine di navigazione
* Tassonomia di navigazione
* Enfasi sulla ricerca

2: la seconda fase della strategia consiste nel comprendere le nozioni di base sull’ottimizzazione, che comprendono la comprensione degli elementi di test stessi. Gli elementi di test di Ottimizzazione includono:

    A. Valore elemento
    
    Questo risultato si ottiene facendo un passo indietro per chiedere perché un determinato elemento esiste sul tuo sito e il contenuto ha uno scopo specifico? Queste domande sono utili se il sito ha appena terminato una riprogettazione o se è stata implementata di recente una nuova funzione. La tattica utilizzata per determinare il valore dell’elemento viene definita test di inclusione/esclusione. Il test di inclusione/esclusione fornisce una buona lettura del valore sulla pagina in cui viene visualizzato l’elemento.
    
     B. Presentazione elemento
    
    In questa sezione è possibile riflettere sull&#39;aspetto generale dell&#39;elemento e su come questo influisce sulla presentazione complessiva della pagina. La tattica utilizzata per la presentazione consiste nell’effettuare modifiche significative a livello di contenuto e di pagina degli elementi.
    
    C. Funzione elemento
    
    La domanda è: l&#39;elemento nella pagina sta facendo quello che dovrebbe fare? L’interazione ha esito positivo e funziona come previsto? L’interazione è naturale o è un punto di attrito? La tattica utilizzata per la funzione consiste nel creare esperienze incentrate su funzionalità di facile utilizzo senza alcun impatto aggiuntivo sui costi.

## Ottimizzazione e personalizzazione

Dopo aver analizzato ed elencato i componenti della strategia, è importante distinguere tra le attività di ottimizzazione e quelle di Personalization. L&#39;ottimizzazione è l&#39;azione di fare l&#39;uso migliore o più efficace di una situazione o di una risorsa, mentre Personalization è l&#39;azione di progettare o produrre qualcosa per soddisfare le esigenze individuali di qualcuno.

Ad alto livello:

* L’ottimizzazione si concentra sui test per individuare ciò che è più efficiente e dalle prestazioni migliori per TUTTI coloro che interagiscono con la presenza digitale.
* Personalization sta testando per trovare ciò che è più efficiente e le prestazioni migliori per alcuni di coloro che interagiscono con la tua presenza digitale.

Quando ci si concentra sull’ottimizzazione, le attività di test più comuni sono:

* **Test A/B:** test in tempo reale di due o più pagine o elementi di pagina tra loro per ottenere insight quantitativo nelle preferenze del cliente.
* **Test multivariato:** confronto di combinazioni di offerte tra gli elementi di una pagina per vedere quale combinazione funziona meglio. Inoltre, il test multivariato identificherà quale elemento della pagina migliora meglio le conversioni.

Quando ti concentri su Personalization, probabilmente visualizzerai le stesse attività di test disponibili in Ottimizzazione, ma sono indirizzate a tipi di pubblico più specifici. Ad esempio, nei test A/B, probabilmente aggiungerai pagine e tipi di pubblico all’interno delle esperienze per promuovere il Personalization.

Personalization include anche il tipo di attività di test Targeting esperienza, che fornisce contenuti a tipi di pubblico specifici in base a una serie di regole e criteri definiti. Man mano che inizi a crescere e ad approfondire la tua esperienza con Personalization, puoi sfruttare alcune delle funzionalità Premium di Target, come:

* Tipo di attività di Automated Personalization
* Tipo di attività consigli

## Ottimizzazione prima della personalizzazione

Alla luce di quanto sopra, Adobe consiglia di ottimizzare prima di personalizzare e passare da Personalization ampio a granulare. Per trasformare le attività di Personalization da grandi a granulari, inizierai a utilizzare uno stile di personalizzazione uno-a-molti (ampio) (utilizzando test A/B), quindi passerai a uno stile di personalizzazione uno-a-uno (granulare) (utilizzando le attività di personalizzazione automatizzata).

Per ulteriori informazioni, leggere il [QuickStart per test di personalizzazione e creazione di roadmap](https://experienceleague.adobe.com/it/perspectives/quickstart-for-personalization-testing-and-roadmap-creation).

Ulteriori informazioni su strategia e leadership di pensiero nell&#39;hub [Perspectives](https://experienceleague.adobe.com/it/perspectives).
