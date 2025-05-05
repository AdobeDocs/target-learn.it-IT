---
title: QuickStart per test di personalizzazione e creazione di roadmap
description: Scopri un framework che puoi utilizzare per iniziare a convalidare le attività di personalizzazione e creare una roadmap di personalizzazione da eseguire tramite Adobe Target e Adobe Analytics.
solution: Target,Analytics
level: Intermediate
role: Leader, Architect, Developer, Admin
exl-id: c0b6f9a0-7074-4e25-81e6-9781a54e2156
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 0%

---

# QuickStart per test di personalizzazione e creazione di roadmap

Personalization può essere potente, ma deve essere convalidato tramite test per garantire che possa davvero generare valore. I test sono la strategia più efficace per identificare chi, come e cosa dovresti personalizzare.

Con l&#39;avvio della seconda decade del 21° secolo, organizzazioni come la vostra si differenziano per strategie di targeting dei consumatori obsolete e analisi dei dati imprecise. Questo è l’inizio della personalizzazione, un’era in cui i consumatori hanno iniziato ad aspettarsi nient’altro che un’esperienza personalizzata. Personalization a livello aziendale è un processo complesso e in continua evoluzione, ma se realizzato in modo efficace, ottimizzerà la soddisfazione dei clienti e aumenterà notevolmente il ROI.

L’articolo seguente fornisce un framework da utilizzare per iniziare a convalidare le attività di personalizzazione e creare una roadmap di personalizzazione da eseguire tramite Adobe Target e Adobe Analytics. Il framework QuickStart di Adobe include:

1. **Identifica opportunità di personalizzazione**: sfrutta l&#39;analisi dei dati per identificare le opportunità di influire sugli indicatori di prestazioni chiave sul sito, legati agli obiettivi aziendali della tua organizzazione.

1. **Sviluppa casi d&#39;uso**: definisci gli obiettivi della tua attività di personalizzazione tenendo presenti gli attributi specifici del visitatore; fai in modo che il contenuto curato migliori l&#39;esperienza del visitatore; stabilisci in anticipo quale sarà l&#39;aspetto del successo e quali azioni possono essere intraprese dagli insegnamenti del test.

1. **Crea una roadmap**: aggrega un elenco e assegna priorità ai casi d&#39;uso di personalizzazione, assicurati che i tuoi sforzi siano concentrati su attività di alto valore; aspettati di perfezionare e rivedere i casi d&#39;uso e la roadmap in base agli insegnamenti.

1. **Progetta ed esegui**: crea e avvia le attività di Adobe Target per distribuire contenuti curati per i tuoi tipi di pubblico prioritari.

1. **Intervieni sui risultati**: analizza le prestazioni dell&#39;attività e riepiloga i risultati, gli approfondimenti, i consigli e i passaggi successivi.

## Passaggio 1: identificare le opportunità di personalizzazione{#personalization}

Questo è il punto di partenza per iniziare a creare la roadmap di Personalization. Quando si esegue un programma di personalizzazione di successo, è essenziale concentrarsi sugli obiettivi aziendali chiave e sugli indicatori di prestazioni chiave. Gli sforzi di Personalization dovrebbero essere allineati di conseguenza per fornire valore. Paul Morris, Adobe Business Consultant, afferma: &quot;Se tutto ciò che fai si inserisce in questi obiettivi, è molto probabile che il tuo programma generi un valore significativo. Tuttavia, se hai un approccio dispersivo ai test, probabilmente troverai alcune vittorie, ma il tuo programma complessivo non avrà quasi lo stesso successo.&quot;

>[!NOTE]
>
>Se non sai immediatamente quali sono i tuoi obiettivi aziendali chiave, è importante identificarli il prima possibile. Assicurati di:


* Stabilisci l’allineamento tra gli obiettivi aziendali e l’ipotesi attuabile. In questo modo è possibile assegnare la priorità ai casi d’uso che offrono il massimo valore alla propria azienda.

* Rendi i tuoi obiettivi misurabili a scopo di tracciamento e correlati all&#39;impatto sui ricavi.

* L’allineamento di ogni opportunità dovrebbe influire su una singola metrica di obiettivo.

A volte puoi avere obiettivi che inizialmente sembrano anche intangibili, come il valore del brand o la fedeltà. È fondamentale poter misurare queste dimensioni per utilizzarle come metriche di obiettivo per le attività di Personalization. In genere, questi tipi di obiettivi possono ancora essere allineati all&#39;impatto sui ricavi, ad esempio il valore del cliente nel corso del ciclo di vita o i costi di acquisizione.Man mano che si progredisce, verificare periodicamente le prestazioni del programma rispetto agli obiettivi aziendali chiave per assicurarsi che il valore venga determinato dal programma Personalization.

Concentrati sull’analisi dei dati per identificare aree specifiche del sito web che possono essere migliorate. L’Adobe consiglia di iniziare con Adobe Analytics per generare casi di utilizzo mirati. Se hai già un team di Analytics, chiedi loro di verificare quanto segue:

1. Tabelle pre-modulo personali: funzione di ideazione che fornisce raggruppamenti illimitati e può aiutarti a rispondere a qualsiasi domanda o ipotesi.
1. Segmentazione avanzata: Segmentation IQ consente di confrontare i visitatori di diverse sezioni del sito.
1. Recensioni giuristiche - Identifica quali parti del tuo sito trarrebbero maggior beneficio da Personalization. Queste recensioni ti consentono di fare un passo indietro e di attraversare il tuo sito come farebbe un cliente.
1. Analisi della concorrenza: è probabile che altre aziende si trovino ad affrontare le stesse sfide che si presentano. Questa analisi non si limita alle società dello stesso settore.

L’obiettivo di questo passaggio è generare informazioni fruibili sotto forma di ipotesi. Un’ipotesi è una previsione creata prima di eseguire un esperimento. Indica chiaramente cosa viene cambiato, cosa pensate che succederà e perché pensate che sia così. L’esecuzione dell’esperimento può dimostrare o confutare l’ipotesi. Al termine di questo passaggio, dovresti disporre di una serie di ipotesi sulle opportunità di personalizzazione che miglioreranno il tuo sito web e la soddisfazione dei visitatori.

## Passaggio 2: sviluppare casi d’uso{#use-cases}

Inizia con le ipotesi generate nel passaggio 1, quindi sviluppa le attività intorno a esse. Ora puoi sviluppare le tabelle pre-modulo create nel passaggio 1A; ciascuno dei KPI ha una serie di ipotesi, che diventano quindi singoli test all’interno di Adobe Target. Se hai difficoltà ad arrivare a questo punto, inizia il più semplicemente possibile, ad esempio concentrandoti sui visitatori di ritorno che frequentano il tuo sito. Pensa ai modi in cui puoi adattare la tua home page ai visitatori che ritornano. Una volta che hai impostato le ipotesi, dovrai definire ogni attività per assegnare un’effettiva priorità a ogni caso d’uso.

1. Definisci i tipi di pubblico prioritari a cui desideri distribuire contenuti personalizzati, tenendo presente gli attributi di visitatore univoci che definiscono chi sono e cosa vogliono (ad esempio, cliente esistente rispetto a cliente potenziale). I desideri e le esigenze dei tipi di pubblico prioritari dovrebbero essere in linea con gli obiettivi aziendali

1. Identifica la posizione specifica nel percorso del visitatore in cui il contenuto personalizzato avrà il maggior impatto. Concentrati sulle pagine in cui potresti aspettarti visitatori da una vasta gamma di utenti tipo o visitatori con diverse esigenze/finalità.

1. Inizia a pianificare un po’ di lavoro di progettazione della variante. I contenuti devono essere curati attentamente in base alle esigenze e ai desideri specifici del pubblico, considerando la posizione in cui si trovano nel loro percorso. Il contenuto giusto deve essere distinto e differenziato.

## Passaggio 3: creare una roadmap, aggregare e assegnare la priorità ai casi d’uso

Aggrega un elenco completo di opportunità di personalizzazione che acquisisce come minimo la posizione, l’idea e la priorità delle attività di personalizzazione.

Il passaggio Prioritizzazione è suddiviso in due fattori:

**Valore:** Utilizza ricerche di settore, benchmark e casi d&#39;uso simili del passato per comprendere il valore previsto che ciascuna delle tue ipotesi potrebbe generare. Desideri che il valore sia collegato direttamente a uno dei tuoi risultati aziendali chiave (KBO) e che sia in un formato standard in modo che ciascuno dei tuoi casi d’uso possa essere confrontato tra loro. Il metodo più comune consiste nell’applicare un valore monetario a ogni caso d’uso a scopo di confronto.

* Costo: esiste un costo naturale associato alla creazione delle varianti di progettazione in Target e quindi al potenziale rollout. Ora è necessario stimare il costo associato a ogni caso d’uso. Il costo include, il tempo e le risorse necessarie per creare esperienze di test, la pianificazione e l’analisi post-test.

L’Adobe consiglia di classificare ciascuno dei casi d’uso su una scala da 1 a 5; con 1 semplice e 5 complesso. Ora disponi di una serie di attività con priorità che puoi testare in Adobe Target. Queste attività costituiranno la base delle tue attività di personalizzazione annuali. L’Adobe consiglia di rivalutare regolarmente la roadmap di Personalization. Gli insegnamenti tratti da ciascuna attività dovrebbero influenzare le priorità della roadmap orientata al futuro. Apprendimenti e consigli avranno un impatto maggiore se verranno attuati in modo tempestivo. Le priorità possono cambiare durante l&#39;anno, ma l&#39;implementazione di una metodologia iterativa assicura sempre la disponibilità di un piano d&#39;azione strategico e la possibilità di tenere traccia degli obiettivi del team e dell&#39;azienda.

## Passaggio 4: Progettare ed eseguire

Sfruttando la documentazione creata per strategizzare il caso di utilizzo della personalizzazione, crea l’attività Personalization in Target per fornire contenuti curati per i tipi di pubblico prioritari. Assicurati che il tipo di attività, le impostazioni, le esperienze e le funzioni di reporting siano allineati agli obiettivi del caso d’uso. La progettazione, il controllo qualità e l’avvio delle attività di personalizzazione sono più efficienti quando rientrano nei processi organizzativi esistenti.

## Passaggio 5: intervenire sui risultati

Una volta che l’attività di personalizzazione ha coinvolto un campione rappresentativo di visitatori, puoi iniziare l’analisi sfruttando le informazioni per guidare i passaggi successivi. Essere guidati dai dati nell’analisi, collegare i consigli all’ipotesi del caso d’uso e illustrare chiaramente l’impatto sugli obiettivi aziendali.

### Ulteriori informazioni

Ti consigliamo di guardare questo video che illustra ciascuno di questi passaggi: [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)

Ulteriori informazioni su strategia e leadership di pensiero nell&#39;hub [Customer Success](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html?lang=it).