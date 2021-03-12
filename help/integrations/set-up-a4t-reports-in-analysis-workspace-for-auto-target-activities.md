---
title: Come impostare rapporti A4T in Analysis Workspace per le attività di Targeting automatico
description: Come configurare i rapporti A4T in Analysis Workspace per ottenere i risultati previsti durante l’esecuzione delle attività di Targeting automatico
kt: null
audience: business user
doc-type: tutorial
activity: use, setup
feature: Analytics for Target (A4T), Targeting automatico
topic: Analytics for Target (A4T), Targeting automatico
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 814ce9b49eff6cbc41a84bb65718f4e5f4f0142d
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---


# Come impostare i rapporti A4T in Analysis Workspace per le attività [!DNL Auto-Target]

L’integrazione di Analytics for Target (A4T) per le attività [!DNL Auto-Target] utilizza gli algoritmi di machine learning (ML) di Adobe Target per scegliere l’esperienza migliore per ogni visitatore in base al suo profilo, comportamento e contesto, il tutto utilizzando una metrica di obiettivo di Adobe Analytics.

Sebbene in Adobe Analytics Analysis Workspace siano disponibili funzionalità di analisi avanzate, alcune modifiche al pannello **[!UICONTROL Analytics for Target]** predefinito sono necessarie per interpretare correttamente le attività [!DNL Auto-Target] a causa delle differenze tra le attività di sperimentazione (A/B manuale e Allocazione automatica) e le attività di personalizzazione ([!DNL Auto-Target]).

Questa esercitazione illustra le modifiche consigliate per l’analisi delle attività [!DNL Auto-Target] in Workspace, basate sui seguenti concetti chiave:

* La dimensione **[!UICONTROL Controllo vs Target]** può essere utilizzata per distinguere tra le esperienze di controllo e quelle servite dall&#39;algoritmo ML di ensemble [!DNL Auto-Target] .
* Le visite devono essere utilizzate come metrica di normalizzazione quando visualizzi le suddivisioni delle prestazioni a livello di esperienza. Inoltre, la metodologia di conteggio predefinita di [Adobe Analytics può includere visite in cui l&#39;utente non visualizza effettivamente il contenuto dell&#39;attività](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics), ma questo comportamento predefinito può essere modificato utilizzando un segmento con ambito appropriato (dettagli qui sotto).
* L’attribuzione con ambito di lookback su visita, nota anche come &quot;intervallo di lookback su visita&quot; sul modello di attribuzione prescritto, viene utilizzata dai modelli ML di Adobe Target durante le fasi di formazione e deve essere utilizzato lo stesso modello di attribuzione (non predefinito) durante la suddivisione della metrica di obiettivo.

## Creare il pannello A4T per [!DNL Auto-Target] in Workspace

Per creare un rapporto A4T per [!DNL Auto-Target], inizia con il pannello **[!UICONTROL Analytics for Target]** in Workspace, come mostrato di seguito, oppure inizia con una tabella a forma libera. Effettua quindi le seguenti selezioni:

1. **[!UICONTROL Controllo esperienza]**: Puoi scegliere qualsiasi esperienza; tuttavia, questa scelta verrà ignorata in un secondo momento. Tieni presente che per le attività [!DNL Auto-Target], l’esperienza di controllo è in realtà una strategia di controllo, ovvero a) Distribuire in modo casuale tra tutte le esperienze, o b) Servire un’unica esperienza (questa scelta viene effettuata al momento della creazione dell’attività in Adobe Target). Anche se hai scelto di scegliere (b), ovvero l’attività [!DNL Auto-Target] che ha designato come controllo un’esperienza specifica, dovresti comunque seguire l’approccio descritto in questa esercitazione per l’analisi di A4T per le attività [!DNL Auto-Target] .
2. **[!UICONTROL Normalizzazione della metrica]**: Seleziona Visite.
3. **[!UICONTROL Metriche]** di successo: Anche se puoi selezionare una metrica o più su cui generare rapporti, in genere dovresti visualizzare i rapporti sulla stessa metrica selezionata per l’ottimizzazione durante la creazione di attività in Adobe Target.

![Figura 1.](assets/Figure1.png)
*pngFigura 1: Configurazione del pannello Analytics for Target per  [!DNL Auto-Target] le attività.*

>[!NOTE]
>
>Per configurare il pannello Analytics for Target per le attività di Targeting automatico, scegli un’esperienza di controllo, scegli Visite come metrica di normalizzazione e scegli la stessa metrica di obiettivo selezionata per l’ottimizzazione durante la creazione di attività Target.

## Utilizza la dimensione Controllo e targeting per confrontare il modello ML dell’insieme di Adobe Target con il tuo controllo

Il pannello A4T predefinito è progettato per test A/B classici (manuali) o attività di allocazione automatica in cui l’obiettivo è quello di confrontare le prestazioni di singole esperienze rispetto all’esperienza di controllo. Nelle attività [!DNL Auto-Target], tuttavia, il primo confronto dovrebbe essere tra la strategia di controllo *a2/> e la strategia di destinazione* a4/> (in altre parole, determinare l&#39;incremento delle prestazioni complessive del modello di raggruppamento ML [!DNL Auto-Target] rispetto alla strategia di controllo).**

Per eseguire questo confronto, utilizza la dimensione **[!UICONTROL Controllo vs Target (Analytics for Target)]** . Trascina per sostituire la dimensione **[!UICONTROL Esperienze di destinazione]** nel rapporto A4T predefinito.

Nota che questa sostituzione invalida i calcoli di incremento e affidabilità predefiniti nel pannello A4T. Per evitare confusione, puoi rimuovere queste metriche dal pannello predefinito, lasciando il seguente rapporto:

![Figura 2.](assets/Figure2.png)
*pngFigura 2: Rapporto di base consigliato per  [!DNL Auto-Target] le attività. Questo rapporto è stato configurato per confrontare il traffico mirato (servito dal modello HTML di insieme) con il traffico di controllo.*

>[!NOTE]
>
>Al momento, i numeri di incremento e affidabilità non sono disponibili per i rapporti Controllo rispetto alle dimensioni di destinazione per A4T per il targeting automatico. Fino a quando non viene aggiunto il supporto, Incremento e Affidabilità possono essere calcolati manualmente scaricando il [calcolatore di affidabilità](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Aggiungere suddivisioni delle metriche a livello di esperienza

Per ulteriori informazioni sulle prestazioni del modello ML di insieme, puoi esaminare le suddivisioni a livello di esperienza della dimensione **[!UICONTROL Controllo rispetto a Target]**. In Workspace, trascina la dimensione **[!UICONTROL Esperienze di Target]** nel rapporto, quindi suddividi separatamente ciascuna delle dimensioni Controllo e Destinazione.

![Figura 3.](assets/Figure3.png)
*pngFigura 3: Suddivisione della dimensione di targeting per esperienze Target*

Un esempio del rapporto risultante è mostrato qui.

![Figura 4.](assets/Figure4.png)
*pngFigura 4: Un  [!DNL Auto-Target] rapporto standard con suddivisioni a livello di esperienza. La metrica di obiettivo può essere diversa e la strategia di controllo può avere una sola esperienza.*

>[!TIP]
>
>In Workspace, fai clic sull’icona a forma di ingranaggio per nascondere le percentuali nella colonna Tasso di conversione, per mantenere lo stato attivo sui tassi di conversione dell’esperienza. I tassi di conversione verranno quindi formattati come decimali, ma interpretati di conseguenza come percentuali.

## Perché &quot;Visite&quot; è la metrica di normalizzazione corretta per le attività [!DNL Auto-Target]

Quando analizzi un’attività [!DNL Auto-Target], scegli sempre Visite come metrica di normalizzazione predefinita. [!DNL Auto-Target] la personalizzazione seleziona un’esperienza per un visitatore una volta per visita (formalmente, una volta per sessione Adobe Target), il che significa che l’esperienza mostrata a un utente può cambiare a ogni singola visita. Pertanto, se utilizzi Visitatori unici come metrica di normalizzazione, il fatto che un singolo utente possa visualizzare più esperienze (in visite diverse) confonderebbe i tassi di conversione.

Un esempio semplice illustra questo punto: considera uno scenario in cui due visitatori accedono a una campagna con solo due esperienze. Il primo visitatore visita due volte. Vengono assegnate all’Esperienza A nella prima visita, ma all’Esperienza B nella seconda visita (a causa della modifica dello stato del profilo in quella seconda visita). Dopo la seconda visita, il visitatore si converte effettuando un ordine. La conversione è attribuita all’esperienza mostrata più di recente (Esperienza B). Anche il secondo visitatore visita due volte e viene mostrato sia l’Esperienza B che la conversione.

Confrontiamo i rapporti a livello di visitatore e di visita:

| Esperienza | Visitatori univoci | Visite | Conversioni | Norma per i visitatori. Conv. Rate | Visita la norma. Conv. Rate |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 3 | 50% | 33,3% |
| Totali | 2 | 4 | 1 | 50% | 25% |
*Tabella 1: Esempio di confronto tra rapporti normalizzati sui visitatori e normalizzati sulle visite per uno scenario in cui le decisioni sono appiccicose a una visita (e non ai visitatori, come con i normali test A/B). Le metriche normalizzate dei visitatori confondono in questo scenario.*

Come mostrato nella tabella, esiste una chiara incongruenza dei numeri a livello di visitatore. Nonostante il fatto che ci siano due visitatori unici totali, questa non è una somma di singoli visitatori unici per ogni esperienza. Anche se il tasso di conversione a livello di visitatore non è necessariamente sbagliato, quando si confrontano le singole esperienze, i tassi di conversione a livello di visita probabilmente hanno molto più senso. Formalmente, l’unità di analisi (&quot;visite&quot;) è la stessa dell’unità di decisione viscerale, il che significa che è possibile aggiungere e confrontare suddivisioni delle metriche a livello di esperienza.

## Filtrare le visite effettive all’attività

La metodologia di conteggio predefinita di Adobe Analytics per le visite a un’attività Target può includere visite in cui l’utente non ha interagito con l’attività Target. Ciò è dovuto al modo in cui le assegnazioni di attività di Target vengono mantenute nel contesto del visitatore di Analytics. Di conseguenza, il numero di visite all’attività Target può talvolta essere gonfiato, con conseguente depressione dei tassi di conversione.

Se preferisci creare rapporti sulle visite in cui l’utente ha effettivamente interagito con l’attività di Targeting automatico (tramite l’accesso all’attività, un evento di visualizzazione/visita o una conversione), puoi:

1. Crea un segmento specifico che include gli hit dall’attività Target in questione, e quindi
1. Filtra la metrica Visite utilizzando questo segmento.

**Per creare il segmento:**

1. Seleziona l’opzione **[!UICONTROL Componenti > Crea segmento]** nella barra degli strumenti di Workspace.
2. Inserisci un **[!UICONTROL Titolo]** per il segmento. Nell’esempio seguente, il segmento si chiama [!DNL "Hit with specific Auto-Target activity"].
3. Trascina la dimensione **[!UICONTROL Attività di Target]** nel segmento **[!UICONTROL Definizione]** .
4. Utilizza l’operatore **[!UICONTROL è uguale a]** .
5. Cerca la tua attività Target specifica.
6. Seleziona l’icona a forma di ingranaggio e seleziona **[!UICONTROL Modello di attribuzione > Istanza]** come mostrato nella figura seguente.
7. Fai clic su **[!UICONTROL Salva]**.

![Figura 5.](assets/Figure5.png)
*pngFigura 5: Utilizza un segmento come quello mostrato qui per filtrare la metrica Visite in A4T per il  [!DNL Auto-Target] rapporto*

Una volta creato il segmento, utilizzalo per filtrare la metrica Visite, in modo che la metrica Visite includa solo le visite in cui l’utente ha interagito con l’attività Target.

**Per filtrare le visite utilizzando questo segmento:**

1. Trascina il segmento appena creato dalla barra degli strumenti dei componenti e passa il cursore del mouse sulla base dell’etichetta della metrica **[!UICONTROL Visite]** finché non viene visualizzato un prompt blu **[!UICONTROL Filtra per]** .
2. Rilascia il segmento. Il filtro verrà applicato a tale metrica.

Il pannello finale verrà visualizzato come segue.

![Figura 6.](assets/Figure6.png)
*pngFigura 6: Pannello di reporting con il segmento &quot;Hit con specifica attività di Targeting automatico&quot; applicato alla metrica   Visitsmetric. Questo assicura che solo le visite in cui un utente ha effettivamente interagito con l&#39;attività Target in questione siano incluse nel rapporto.*

## Allinea l’attribuzione tra la formazione sul modello ML e la generazione della metrica obiettivo

L’integrazione A4T consente al modello ML di [!DNL Auto-Target] di essere *addestrato* utilizzando gli stessi dati evento di conversione utilizzati da Adobe Analytics per *generare rapporti sulle prestazioni*. Tuttavia, vi sono alcune ipotesi che devono essere utilizzate per interpretare questi dati durante la formazione dei modelli ML, che differiscono dalle ipotesi di default formulate durante la fase di segnalazione in Adobe Analytics.

In particolare, i modelli ML di Adobe Target utilizzano un modello di attribuzione basato sulle visite. In altre parole, presuppongono che una conversione avvenga nella stessa visita di una visualizzazione del contenuto per l&#39;attività, affinché la conversione sia &quot;attribuita&quot; alla decisione presa dal modello ML. Ciò è necessario affinché Target garantisca una formazione tempestiva dei suoi modelli; Target non può attendere fino a 30 giorni per una conversione (la finestra di attribuzione predefinita per i rapporti in Adobe Analytics), prima di includerla nei dati di formazione per i suoi modelli.

Pertanto, la differenza tra l’attribuzione utilizzata dai modelli di Target (durante la formazione) e l’attribuzione predefinita utilizzata per eseguire query sui dati (durante la generazione del rapporto) può causare discrepanze. Potrebbe anche sembrare che i modelli ML abbiano prestazioni scadenti, quando in realtà il problema è legato all&#39;attribuzione.

>[!TIP]
>
>Se i modelli ML vengono ottimizzati per una metrica che viene attribuita in modo diverso rispetto alle metriche visualizzate in un rapporto, le prestazioni dei modelli potrebbero non essere quelle previste. Per evitare questo problema, assicurati che le metriche dell’obiettivo nel rapporto utilizzino la stessa attribuzione utilizzata dai modelli ML di Target.

Per visualizzare le metriche dell’obiettivo che hanno la stessa metodologia di attribuzione utilizzata dai modelli ML di Adobe Target, procedi come segue:

1. Passa il puntatore sull’icona a forma di ingranaggio della metrica di obiettivo:
   ![gearicon.png](assets/gearicon.png)
1. Dal menu risultante, scorri fino a **[!UICONTROL Impostazioni dati]**.
1. Seleziona **[!UICONTROL Usa modello di attribuzione non predefinito]** (se non è già selezionato):
   ![non defaultattributionmodel.png](assets/non-defaultattributionmodel.png)
1. Fare clic su **[!UICONTROL Modifica]**.
1. Seleziona **[!UICONTROL Modello]**: **[!UICONTROL Partecipazione]** e **[!UICONTROL Intervallo di lookback]**: **[!UICONTROL Visita]**.
   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)
1. Fai clic su **[!UICONTROL Applica]**.

Questi passaggi garantiscono che il rapporto attribuisca la metrica di obiettivo alla visualizzazione dell’esperienza, se l’evento di metrica di obiettivo si è verificato *in qualsiasi momento* (&quot;partecipazione&quot;) nella stessa visita in cui è stata mostrata un’esperienza.

## Passaggio finale: Crea un tasso di conversione che cattura la magia di cui sopra

Con le modifiche alle metriche Visita e obiettivo nelle sezioni precedenti, l’ultima modifica da apportare al pannello di reporting A4T predefinito per [!DNL Auto-Target] è quella di creare tassi di conversione che siano il rapporto corretto, quello di una metrica di obiettivo con la giusta attribuzione, a una metrica &quot;Visite&quot; filtrata in modo appropriato.

A tale scopo, crea una metrica calcolata utilizzando i seguenti passaggi:

1. Seleziona l’opzione **[!UICONTROL Componenti > Crea metrica]** nella barra degli strumenti di Workspace.
1. Immetti un **[!UICONTROL Titolo]** per la metrica. Ad esempio, &quot;Tasso di conversione corretto per le visite per l’attività XXX&quot;.
1. Seleziona **[!UICONTROL Formato]** = Percentuale e **[!UICONTROL Posizioni decimali]** = 2.
1. Trascina la metrica di obiettivo pertinente per l’attività (ad esempio, Conversioni attività) nella definizione e utilizza l’icona a forma di ingranaggio su questa metrica di obiettivo per regolare il modello di attribuzione su (Partecipazione|Visita), come descritto in precedenza.
1. Seleziona **[!UICONTROL Aggiungi > Contenitore]** in alto a destra della sezione **[!UICONTROL Definizione]** .
1. Selezionare l&#39;operatore di divisione (÷) tra i due contenitori.
1. Trascina il segmento creato in precedenza, denominato &quot;Hit with Specific [!DNL Auto-Target] activity&quot; in questa esercitazione, per questa specifica attività [!DNL Auto-Target].
1. Trascina la metrica **[!UICONTROL Visite]** nel contenitore segmenti.
1. Fai clic su **[!UICONTROL Salva]**.

La definizione completa della metrica calcolata è mostrata qui.

![Figura 7.](assets/Figure7.png)
*pngFigura 7: Definizione della metrica del tasso di conversione del modello corretta per visita e attribuzione. (Nota che questa metrica dipende dalla metrica e dall’attività dell’obiettivo. In altre parole, questa definizione di metrica non è riutilizzabile tra le attività.)*

>[!IMPORTANT]
>
>La metrica del tasso di conversione dal pannello A4T non è collegata all’evento di conversione o alla metrica di normalizzazione nella tabella. Quando apporti le modifiche suggerite in questa esercitazione, il tasso di conversione non si adatta automaticamente alle modifiche. Pertanto, se apporti la modifica a uno (o entrambi) l’attribuzione dell’evento di conversione e la metrica di normalizzazione, devi ricordare come passaggio finale per modificare anche il tasso di conversione, come mostrato sopra.

## Riepilogo: Pannello Area di lavoro di esempio finale per i report [!DNL Auto-Target]

Combinando tutti i passaggi precedenti in un singolo pannello, la figura seguente mostra una visualizzazione completa del rapporto consigliato per le attività [!DNL Auto-Target] A4T. Questo rapporto è lo stesso utilizzato dai modelli di machine learning di Target per ottimizzare la metrica dell’obiettivo e include tutte le sfumature e i consigli descritti in questa esercitazione. Questo rapporto è anche più vicino alle metodologie di conteggio utilizzate nelle attività tradizionali di reporting basate su Target [!DNL Auto-Target].

![Figura 8.](assets/Figure8.png)
*pngFigura 8: Il  [!DNL Auto-Target] rapporto finale A4T in Adobe Analytics Workspace, che combina tutte le modifiche alle definizioni metriche descritte nelle sezioni precedenti di questo documento.*
