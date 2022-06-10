---
title: QuickStart per test di personalizzazione e creazione di roadmap
description: 'Scopri un framework che puoi utilizzare per iniziare a convalidare le attività di personalizzazione e crea una roadmap di personalizzazione da eseguire tramite Adobe Target e Adobe Analytics.  '
solution: Target,Analytics
source-git-commit: fd679d3fc2c72b9852d8129adf8c1187bf22b25f
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# QuickStart per test di personalizzazione e creazione di roadmap

La personalizzazione può essere potente, ma deve essere convalidata tramite test per garantire che produca davvero valore. Il test è la strategia più efficace per identificare chi, come e cosa personalizzare.

Con il lancio nel secondo decennio del XXI secolo, organizzazioni come la vostra stanno separando i modi con strategie di targeting dei consumatori obsolete e con un&#39;analisi dei dati imprecisa. Questa è l&#39;alba della personalizzazione, un&#39;era in cui i consumatori si sono aspettati niente di meno che un&#39;esperienza personalizzata. La personalizzazione a livello aziendale è un processo complesso e in continua evoluzione, ma una volta fatto in modo efficace, massimizza la soddisfazione dei clienti e aumenta notevolmente il ROI.

Il seguente articolo fornisce un framework che puoi utilizzare per iniziare a convalidare le attività di personalizzazione e creare una roadmap di personalizzazione da eseguire tramite Adobe Target e Adobe Analytics. Il framework QuickStart di Adobe include:

1. **Identificare le opportunità di personalizzazione** : sfrutta l’analisi dei dati per identificare le opportunità di influenzare gli indicatori prestazioni chiave sul sito, in base agli obiettivi aziendali della tua organizzazione.

1. **Sviluppare casi di utilizzo** - definisci gli obiettivi dell’attività di personalizzazione tenendo presenti attributi specifici del visitatore, essere esplicito su come il contenuto curato migliorerà l’esperienza del visitatore, stabilire in anticipo come si presenterà il successo e quali azioni possono essere intraprese dagli apprendisti del test.

1. **Creare una roadmap** - aggregare un elenco e assegnare priorità ai casi di utilizzo della personalizzazione, assicurarsi che i vostri sforzi siano incentrati su attività di alto valore; si aspetta di perfezionare e rivedere i casi di utilizzo e la roadmap in base agli insegnamenti.

1. **Progettazione ed esecuzione** - crea e avvia le attività di Adobe Target per fornire contenuti curati per i tipi di pubblico prioritari.

1. **Intervenire sui risultati** - analizzare le prestazioni dell’attività e riepilogare i risultati dell’attività, le informazioni, i consigli e i passaggi successivi.

## Passaggio 1: Identificare le opportunità di personalizzazione{#personalization}

Questo è il punto di partenza da cui iniziare a formare la Roadmap sulla Personalizzazione. Quando si esegue un programma di personalizzazione di successo, è essenziale concentrarsi sugli obiettivi aziendali chiave e sugli indicatori di prestazioni chiave. Gli sforzi di personalizzazione devono essere allineati di conseguenza per fornire valore. Paul Morris, Adobe Business Consultant, afferma: &quot;Se tutto ciò che fai si nutre di questi obiettivi, è molto probabile che il tuo programma dia un valore significativo. Tuttavia, se hai un approccio sparso al test, probabilmente troverai alcune vittorie, ma il tuo programma complessivo non avrà quasi successo.&quot;

>[!NOTE]
>
>Se non sai immediatamente quali sono i tuoi obiettivi aziendali chiave, è importante identificarli il prima possibile. Assicurati di:


* Stabilire l&#39;allineamento tra gli obiettivi aziendali e l&#39;ipotesi attuabile. In questo modo puoi assegnare priorità ai casi di utilizzo che forniscono il massimo valore alla tua azienda.

* Rendi i tuoi obiettivi misurabili a scopo di tracciamento e correlati all&#39;impatto sui ricavi.

* Allinea ogni opportunità dovrebbe avere un impatto su una singola metrica dell’obiettivo.

A volte si possono avere obiettivi che inizialmente sembrano immateriali, come il valore del marchio o la fedeltà. È fondamentale che tu sia in grado di misurarle al fine di utilizzarle come metriche di obiettivo per le attività di personalizzazione. In genere, questi tipi di obiettivi possono ancora essere allineati all&#39;impatto sui ricavi, ad esempio il valore del cliente a vita o i costi di acquisizione. Durante l&#39;avanzamento, assicurati di controllare periodicamente le prestazioni del programma rispetto agli obiettivi aziendali chiave per assicurarsi che il valore sia guidato dal programma di personalizzazione.

Attiva l’analisi dei dati per identificare aree specifiche del sito web che possono essere migliorate. Adobe consiglia di iniziare con Adobe Analytics per generare casi di utilizzo mirati. Se hai un team Analytics attivo, chiedi loro di esaminare quanto segue:

1. Tabelle pre-modulo personali : una funzione di identificazione che fornisce raggruppamenti illimitati e può essere utile per rispondere a eventuali domande o ipotesi.
1. Segmentazione avanzata: la segmentazione IQ consente di confrontare i visitatori di diverse sezioni del sito.
1. Recensioni giuristiche - Identifica quali parti del tuo sito trarrebbero maggior beneficio dalla Personalizzazione. Queste recensioni ti permettono di fare un passo indietro e di attraversare il tuo sito come farebbe un cliente.
1. Analisi della concorrenza : le probabilità sono che altre aziende affrontino le stesse sfide che si pongono. Tale analisi non si limita alle imprese dello stesso settore.

L&#39;obiettivo di questo passaggio è quello di generare informazioni fruibili sotto forma di ipotesi. Un&#39;ipotesi è una previsione che si crea prima di eseguire un esperimento. Indica chiaramente cosa viene cambiato, cosa credete che sarà il risultato e perché pensate che sia così. Eseguire l&#39;esperimento dimostrerà o confuterà la tua ipotesi. Al termine di questo passaggio, dovresti avere una serie di ipotesi sulle opportunità di personalizzazione che miglioreranno la soddisfazione del tuo sito web e del visitatore.

## Passaggio 2: Sviluppare casi di utilizzo{#use-cases}

Inizia con le ipotesi generate nel passaggio 1, quindi sviluppa le tue attività intorno a loro. È ora possibile sviluppare le tabelle pre-form create nel passaggio 1A; ciascuno dei KPI presenta una serie di ipotesi che diventano poi singoli test in Adobe Target. Se hai difficoltà a raggiungere questo punto, inizia il più semplicemente possibile, ad esempio concentrandoti sui visitatori di ritorno che frequentano il tuo sito. Pensa ai modi in cui puoi adattare la tua homepage ai visitatori di ritorno. Una volta che hai impostato il tuo set di ipotesi, dovrai definire ogni attività per assegnare una priorità efficace a ogni caso di utilizzo.

1. Definisci i tipi di pubblico prioritari a cui desideri indirizzare i contenuti personalizzati, tenendo conto degli attributi univoci dei visitatori che definiscono chi sono e cosa desiderano (ad esempio, clienti esistenti o potenziali) I desideri e le esigenze dei tipi di pubblico prioritari devono essere allineati agli obiettivi aziendali

1. Identifica la posizione specifica nel percorso del visitatore in cui i contenuti personalizzati avranno il maggiore impatto. Concentrati sulle pagine in cui ti aspetteresti visitatori di diverse persone o visitatori con varie esigenze/intenzioni.

1. Inizia a pianificare un lavoro di progettazione della tua variante. I contenuti devono essere attentamente curati in base alle esigenze e ai desideri specifici del pubblico, considerando dove si trovano nel loro percorso. Il contenuto giusto dovrebbe essere distinto e differenziato.

## Passaggio 3: Creare una roadmap, aggregare e assegnare priorità ai casi di utilizzo

Aggrega un elenco completo di opportunità di personalizzazione che acquisisca al minimo la posizione, l’idea e la priorità delle attività di personalizzazione.

La fase Priorità è suddivisa in due fattori:

**Valore:** Utilizza ricerche di settore, analisi comparativa e casi d&#39;uso simili del passato per capire il valore atteso che ciascuna delle tue ipotesi può dare. Desideri che il tuo valore sia collegato direttamente a uno dei tuoi KBO (Key Business Outcome) e sia in un formato standard in modo che ciascuno dei tuoi casi d&#39;uso possa essere confrontato l&#39;uno con l&#39;altro. Il metodo più comune è quello di applicare un valore monetario a ogni caso d&#39;uso per un confronto.

* Costo: esiste un costo naturale associato alla creazione delle varianti di progettazione all’interno di Target e quindi al potenziale rollout. Ora dovrai stimare il costo associato a ciascun caso d’uso. Il costo include, il tempo e le risorse necessari per creare esperienze di test, la pianificazione e l’analisi post-test.

L’Adobe consiglia di classificare ciascuno dei casi d’uso in una scala da 1 a 5; 1 semplice e 5 complesso. Ora disponi di un set di attività con priorità da testare in Adobe Target. Queste attività formeranno la base delle attività di personalizzazione annuali. L’Adobe consiglia di rivalutare regolarmente la roadmap sulla personalizzazione. Gli insegnamenti tratti da ogni attività dovrebbero influenzare le priorità della roadmap verso il futuro. Gli insegnamenti e le raccomandazioni avranno un maggiore impatto se verranno presi in considerazione in tempi brevi. Le priorità durante tutto l&#39;anno possono cambiare, ma l&#39;esecuzione di una metodologia iterativa assicura che tu abbia sempre un piano d&#39;azione strategico in atto e che tu possa tenere traccia contro i tuoi obiettivi del team e dell&#39;azienda.

## Passaggio 4: Progettazione ed esecuzione

Sfruttando la documentazione creata per strategizzare il caso d’uso della personalizzazione, crea l’attività di personalizzazione all’interno di Target per fornire contenuti curati per i tipi di pubblico prioritari. Assicurati che il tipo di attività, le impostazioni, le esperienze e le funzioni di reporting siano allineate agli obiettivi del caso d’uso. La progettazione, il controllo qualità e il lancio del tuo sforzo di personalizzazione sono i più efficienti quando l’utente rientra nei processi aziendali esistenti.

## Passaggio 5: Intervenire sui risultati

Una volta che l’attività di personalizzazione ha coinvolto un campione rappresentativo di visitatori, puoi iniziare l’analisi sfruttando le informazioni per guidare i passaggi successivi. Sii guidato dai dati nell’analisi, associa i consigli all’ipotesi del tuo caso d’uso e illustra chiaramente l’impatto sugli obiettivi aziendali.

### Ulteriori informazioni

È consigliabile guardare questo video che illustra ciascuno di questi passaggi: [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)