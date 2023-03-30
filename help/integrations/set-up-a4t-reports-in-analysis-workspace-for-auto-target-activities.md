---
title: Come impostare i rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Target] Attività
description: Come configurare i rapporti A4T in [!DNL Analysis Workspace] per ottenere i risultati previsti durante l'esecuzione [!UICONTROL Targeting automatico] attività?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium newtab=true" tooltip="See what's included in Target Premium."
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 04327a87db4ad4aa821b64d432e7278c3d55842c
workflow-type: tm+mt
source-wordcount: '2641'
ht-degree: 1%

---

# Configurazione dei rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Target] attività

>[!IMPORTANT]
>
>Per [!UICONTROL Targeting automatico] attività, è necessario controllare il reporting in [!DNL Analytics Workspace] e creare manualmente un pannello A4T.

La [!UICONTROL Analytics for Target] Integrazione (A4T) per [!DNL Auto-Target] le attività utilizzano [!DNL Adobe Target] riunire gli algoritmi di machine learning (ML) per scegliere l&#39;esperienza migliore per ogni visitatore in base al suo profilo, comportamento e contesto, il tutto mentre utilizza un [!DNL Adobe Analytics] metrica di obiettivo.

Sebbene siano disponibili funzionalità avanzate di analisi in [!DNL Adobe Analytics] [!DNL Analysis Workspace], alcune modifiche all&#39;impostazione predefinita **[!UICONTROL Analytics for Target]** Il pannello è necessario per interpretare correttamente [!DNL Auto-Target] attività, a causa di differenze tra le attività di sperimentazione (manuale [!UICONTROL Test A/B] e [!UICONTROL Allocazione automatica]) e attività di personalizzazione ([!UICONTROL [!UICONTROL Targeting automatico]]).

Questa esercitazione illustra le modifiche consigliate per l&#39;analisi [!UICONTROL Targeting automatico] attività [!DNL Analysis Workspace], che si basano sui seguenti concetti chiave:

* La **[!UICONTROL Controllo e targeting]** può essere utilizzata per distinguere tra [!UICONTROL Controllo] esperienze rispetto a quelle servite dal [!UICONTROL Targeting automatico] algoritmo ML di raggruppamento.
* Le visite devono essere utilizzate come metrica di normalizzazione quando visualizzi le suddivisioni delle prestazioni a livello di esperienza. Inoltre, [La metodologia di conteggio predefinita di Adobe Analytics può includere visite in cui l’utente non visualizza effettivamente il contenuto dell’attività](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html#metrics){target=_blank}, ma questo comportamento predefinito può essere modificato utilizzando un segmento con ambito appropriato (dettagli qui sotto).
* L’attribuzione dell’ambito di lookback per visita, nota anche come &quot;intervallo di lookback per visita&quot; sul modello di attribuzione prescritto, viene utilizzata dal [!DNL Adobe Target] I modelli ML durante le fasi di formazione e lo stesso modello di attribuzione (non predefinito) devono essere utilizzati per suddividere la metrica obiettivo.

## Creare A4T per [!UICONTROL Targeting automatico] pannello in [!DNL Analysis Workspace]

Per creare un A4T per [!UICONTROL Targeting automatico] inizia con **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace], come illustrato di seguito, o inizia con una tabella a forma libera. Effettua quindi le seguenti selezioni:

1. **[!UICONTROL Control Experience]**: Puoi scegliere qualsiasi esperienza; tuttavia, questa scelta verrà ignorata in un secondo momento. Tieni presente che per [!UICONTROL Targeting automatico] attività, l&#39;esperienza di controllo è in realtà una strategia di controllo, che è a) servire casualmente tra tutte le esperienze, o b) Servire una singola esperienza (questa scelta viene effettuata al momento della creazione dell&#39;attività in [!DNL Adobe Target]). Anche se hai scelto la scelta (b), la tua [!UICONTROL Targeting automatico] attività ha designato come controllo un’esperienza specifica. È comunque necessario seguire l’approccio descritto in questa esercitazione per l’analisi di A4T per [!UICONTROL Targeting automatico] attività.
2. **[!UICONTROL Normalizzazione della metrica]**: Seleziona [!UICONTROL Visite].
3. **[!UICONTROL Metriche di successo]**: Sebbene sia possibile selezionare qualsiasi metrica su cui creare rapporti, in genere è necessario visualizzare i rapporti sulla stessa metrica selezionata per l’ottimizzazione durante la creazione di attività in [!DNL Target].

   ![[!UICONTROL Analytics for Target] configurazione del pannello per [!UICONTROL Targeting automatico] attività.](assets/Figure1.png)

   *Figura 1: [!UICONTROL Analytics for Target] configurazione del pannello per [!UICONTROL Targeting automatico] attività.*

>[!TIP]
>
>Per configurare il [!UICONTROL Analytics for Target] pannello per [!UICONTROL Targeting automatico] attività, scegli qualsiasi esperienza di controllo, scegli [!UICONTROL Visite] come metrica di normalizzazione e scegli la stessa metrica di obiettivo selezionata per l’ottimizzazione durante [!DNL Target] creazione di attività.

## Utilizza la [!UICONTROL Controllo vs. Target] dimensione per confrontare [!DNL Target] mettere insieme il modello ML al controllo

Il pannello A4T predefinito è progettato per l’interfaccia classica (manuale) [!UICONTROL Test A/B] o [!UICONTROL Allocazione automatica] attività in cui l’obiettivo è confrontare le prestazioni di singole esperienze rispetto all’esperienza di controllo. In [!UICONTROL Targeting automatico] le attività, tuttavia, il confronto di primo ordine dovrebbe essere tra il controllo *strategia* e la destinazione *strategia*. In altre parole, determinare l&#39;incremento delle prestazioni complessive del [!UICONTROL Targeting automatico] mettere insieme il modello ML sulla strategia di controllo.

Per eseguire questo confronto, utilizza la variabile **[!UICONTROL Controllo e targeting (Analytics for Target)]** dimensione. Trascina e rilascia per sostituire **[!UICONTROL Esperienze Target]** nel rapporto A4T predefinito.

Nota: questa sostituzione invalida il valore predefinito [!UICONTROL Incremento e affidabilità] nel pannello A4T. Per evitare confusione, puoi rimuovere queste metriche dal pannello predefinito, lasciando il seguente rapporto:

![[!UICONTROL Esperienze per conversioni di attività] pannello in [!DNL Analysis Workspace]](assets/Figure2.png)

*Figura 2: Rapporto di base consigliato per [!DNL Auto-Target] attività. Questo rapporto è stato configurato per confrontare il traffico di destinazione (gestito dal modello ML dell’insieme) con il traffico di controllo.*

>[!NOTE]
>
>Attualmente, [!UICONTROL Incremento e affidabilità] i numeri non sono disponibili per [!UICONTROL Controllo e targeting] dimensioni per i rapporti A4T per [!UICONTROL Targeting automatico]. Fino all&#39;aggiunta del supporto, [!UICONTROL Incremento e affidabilità] può essere calcolato manualmente scaricando il [calcolatore di affidabilità](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx).

## Aggiungere suddivisioni delle metriche a livello di esperienza

Per ottenere ulteriori informazioni sulle prestazioni del modello ML di insieme, puoi esaminare le suddivisioni a livello di esperienza **[!UICONTROL Controllo e targeting]** dimensione. In [!DNL Analysis Workspace], trascina **[!UICONTROL Esperienze Target]** inserisci le dimensioni nel rapporto, quindi suddividi separatamente ciascun controllo e ciascuna dimensione di destinazione.

![[!UICONTROL Esperienze per conversioni di attività] pannello in [!DNL Analysis Workspace]](assets/Figure3.png)

*Figura 3: Suddivisione della dimensione di targeting per esperienze Target*

Un esempio del rapporto risultante è mostrato qui.

![[!UICONTROL Esperienze per conversioni di attività] pannello in [!DNL Analysis Workspace]](assets/Figure4.png)

*Figura 4: Standard [!UICONTROL Targeting automatico] rapporti con suddivisioni a livello di esperienza. Tieni presente che la metrica di obiettivo potrebbe essere diversa e che la strategia di controllo potrebbe avere una sola esperienza.*

>[!TIP]
>
>In [!DNL Analysis Workspace], fai clic sull’icona a forma di ingranaggio per nascondere le percentuali nel [!UICONTROL Tasso di conversione] per mantenere lo stato attivo sui tassi di conversione dell’esperienza. I tassi di conversione verranno quindi formattati come decimali, ma interpretati di conseguenza come percentuali.

## Perché &quot;[!UICONTROL Visite]&quot; è la metrica di normalizzazione corretta per [!UICONTROL Targeting automatico] attività

Quando si analizza un [!UICONTROL Targeting automatico] attività, scegli sempre [!UICONTROL Visite] come metrica di normalizzazione predefinita. [!UICONTROL Targeting automatico] la personalizzazione seleziona un’esperienza per un visitatore una volta per visita (formalmente, una volta per visita) [!DNL Target] (sessione), il che significa che l’esperienza mostrata a un visitatore può cambiare in ogni singola visita. Pertanto, se utilizzi [!UICONTROL Visitatori unici] come metrica di normalizzazione, il fatto che un singolo utente possa visualizzare più esperienze (in visite diverse) confonderebbe i tassi di conversione.

Un esempio semplice illustra questo punto: considera uno scenario in cui due visitatori accedono a una campagna con solo due esperienze. Il primo visitatore visita due volte. Vengono assegnate all’Esperienza A nella prima visita, ma all’Esperienza B nella seconda visita (a causa della modifica dello stato del profilo in quella seconda visita). Dopo la seconda visita, il visitatore si converte effettuando un ordine. La conversione è attribuita all’esperienza mostrata più di recente (Esperienza B). Anche il secondo visitatore visita due volte e viene mostrato sia l’Esperienza B che la conversione.

Confrontiamo i rapporti a livello di visitatore e di visita:

| Esperienza | Visitatori univoci | Visite | Conversioni | Tasso di conversione normalizzato del visitatore | Tasso di conversione normalizzato per le visite |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| Totali | 2 | 4 | 1 | 50% | 25% |

*Tabella 1: Esempio di confronto tra rapporti normalizzati sui visitatori e normalizzati sulle visite per uno scenario in cui le decisioni sono appiccicose a una visita (e non ai visitatori, come con i normali test A/B). Le metriche normalizzate dai visitatori confondono in questo scenario.*

Come mostrato nella tabella, esiste una chiara incongruenza dei numeri a livello di visitatore. Nonostante il fatto che ci siano due visitatori unici totali, questa non è una somma di singoli visitatori unici per ogni esperienza. Anche se il tasso di conversione a livello di visitatore non è necessariamente sbagliato, quando si confrontano le singole esperienze, i tassi di conversione a livello di visita hanno probabilmente più senso. Formalmente, l’unità di analisi (&quot;visite&quot;) è identica all’unità di decisione visiva, il che significa che è possibile aggiungere e confrontare suddivisioni delle metriche a livello di esperienza.

## Filtrare le visite effettive all’attività

La [!DNL Adobe Analytics] metodologia di conteggio predefinita per le visite a un [!DNL Target] l’attività potrebbe includere visite in cui l’utente non ha interagito con [!DNL Target] attività. Questo è dovuto al modo [!DNL Target] le assegnazioni di attività vengono mantenute nella [!DNL Analytics] contesto del visitatore. Di conseguenza, il numero di visite al [!DNL Target] A volte l&#39;attività può essere gonfiata, con conseguente depressione dei tassi di conversione.

Se preferisci creare rapporti sulle visite in cui l’utente ha effettivamente interagito con il [!UICONTROL Targeting automatico] tramite l’accesso all’attività, un evento di visualizzazione o visita o una conversione, puoi:

1. Crea un segmento specifico che include gli hit dalla [!DNL Target] attività in questione, e
1. Filtrare [!UICONTROL Visite] utilizzando questo segmento.

**Per creare il segmento:**

1. Seleziona la **[!UICONTROL Componenti > Crea segmento]** in [!DNL Analysis Workspace] barra degli strumenti.
2. Specifica una **[!UICONTROL Titolo]** per il segmento. Nell’esempio seguente, il segmento viene denominato [!DNL "Hit with specific Auto-Target activity"].
3. Trascina **[!UICONTROL Attività di Target]** Dimensione del segmento **[!UICONTROL Definizione]** sezione .
4. Utilizza la **[!UICONTROL è]** operatore.
5. Cerca le tue specifiche [!DNL Target] attività.
6. Fai clic sull’icona a forma di ingranaggio, quindi seleziona **[!UICONTROL Modello di attribuzione > Istanza]** come illustrato nella figura riportata di seguito.
7. Fai clic su **[!UICONTROL Salva]**.

![Segmento in [!DNL Analysis Workspace]](assets/Figure5.png)

*Figura 5: Utilizza un segmento come quello mostrato qui per filtrare il [!UICONTROL Visite] metrica in A4T per [!UICONTROL Targeting automatico] rapporto*

Una volta creato il segmento, utilizzalo per filtrare il [!UICONTROL Visite] quindi la metrica [!UICONTROL Visite] include solo le visite in cui l’utente ha interagito con [!DNL Target] attività.

**Per filtrare [!UICONTROL Visite] utilizzando questo segmento:**

1. Trascina il segmento appena creato dalla barra degli strumenti dei componenti e passa il puntatore del mouse sulla base della **[!UICONTROL Visite]** etichetta metrica fino a un blu **[!UICONTROL Filtra per]** viene visualizzato un prompt.
2. Rilascia il segmento. Il filtro viene applicato a tale metrica.

Il pannello finale viene visualizzato come segue:

![[!UICONTROL Esperienze per conversioni di attività] pannello in [!DNL Analysis Workspace]](assets/Figure6.png)

*Figura 6: Pannello di reporting con il segmento &quot;Hit con specifica attività di Targeting automatico&quot; applicato al [!UICONTROL Visite] metrica. Questo segmento assicura che solo le visite in cui un utente ha effettivamente interagito con [!DNL Target] Le attività in questione sono incluse nel rapporto.*

## Assicurati che la metrica di obiettivo e l’attribuzione siano allineate con il criterio di ottimizzazione

L’integrazione A4T consente [!UICONTROL Targeting automatico] Modello ML da utilizzare *addestrato* utilizzando gli stessi dati evento di conversione che [!DNL Adobe Analytics] utilizza *generare rapporti sulle prestazioni*. Tuttavia, vi sono alcune ipotesi che devono essere utilizzate per interpretare questi dati durante la formazione dei modelli ML, che differiscono dalle ipotesi di default formulate durante la fase di segnalazione in [!DNL Adobe Analytics].

In particolare, [!DNL Adobe Target] I modelli ML utilizzano un modello di attribuzione con ambito visita. In altre parole, i modelli ML presuppongono che una conversione debba avvenire nella stessa visita di una visualizzazione del contenuto per l&#39;attività, affinché la conversione sia &quot;attribuita&quot; alla decisione presa dal modello ML. Questo è necessario per [!DNL Target] garantire una formazione tempestiva dei suoi modelli; [!DNL Target] non può attendere fino a 30 giorni per una conversione (la finestra di attribuzione predefinita per i rapporti in [!DNL Adobe Analytics]) prima di includerlo nei dati di formazione per i suoi modelli.

Pertanto, la differenza tra l’attribuzione utilizzata dal [!DNL Target] i modelli (durante la formazione) rispetto all’attribuzione predefinita utilizzata nelle query dei dati (durante la generazione del rapporto) potrebbero causare discrepanze. Potrebbe anche sembrare che i modelli ML abbiano prestazioni scadenti, quando in realtà il problema è legato all&#39;attribuzione.

>[!TIP]
>
>Se i modelli ML vengono ottimizzati per una metrica che viene attribuita in modo diverso rispetto alle metriche visualizzate in un rapporto, le prestazioni dei modelli potrebbero non essere quelle previste. Per evitare questo problema, accertati che le metriche dell’obiettivo nel rapporto utilizzino la stessa definizione metrica e attribuzione utilizzata dal [!DNL Target] Modelli ML.

La definizione esatta della metrica e le impostazioni di attribuzione dipendono dal [criterio di ottimizzazione](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank} hai specificato durante la creazione dell’attività.

### Conversioni definite da Target, o [!DNL Analytics] metriche con *Massimizza valore della metrica per visita*

Quando la metrica è un [!DNL Target] o un [!DNL Analytics] metriche con **Massimizza valore della metrica per visita**, la definizione della metrica obiettivo consente di verificare più eventi di conversione nella stessa visita.

Per visualizzare le metriche dell’obiettivo con la stessa metodologia di attribuzione utilizzata dalla [!DNL Target] Modelli ML, seguire questi passaggi:

1. Passa il puntatore sull’icona a forma di ingranaggio della metrica di obiettivo:

   ![gearicon.png](assets/gearicon.png)

1. Dal menu risultante, scorri fino a **[!UICONTROL Impostazioni dati]**.
1. Seleziona **[!UICONTROL Usa modello di attribuzione non predefinito]** (se non è già selezionato).

   ![non defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Fai clic su **[!UICONTROL Modifica]**.
1. Seleziona **[!UICONTROL Modello]**: **[!UICONTROL Partecipazione]** e **[!UICONTROL Intervallo di lookback]**: **[!UICONTROL Visita]**.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. Fai clic su **[!UICONTROL Applica]**.

Questi passaggi assicurano che il rapporto attribuisca la metrica di obiettivo alla visualizzazione dell’esperienza, se si è verificato l’evento della metrica di obiettivo *qualsiasi ora* (&quot;partecipazione&quot;) nella stessa visita in cui è stata mostrata un’esperienza.

### [!DNL Analytics] metriche con *Tassi di conversione delle visite univoci*

**Definire la visita con un segmento di metrica positiva**

Nello scenario in cui hai selezionato *Massimizza il tasso di conversione della visita univoca* come criterio di ottimizzazione, la definizione corretta del tasso di conversione è la frazione di visite in cui il valore della metrica è positivo. Questo può essere ottenuto creando un segmento che filtra verso il basso le visite con un valore positivo della metrica, e quindi filtrando la metrica visite.

1. Come prima, seleziona la **[!UICONTROL Componenti > Crea segmento]** in [!DNL Analysis Workspace] barra degli strumenti.
2. Specifica una **[!UICONTROL Titolo]** per il segmento.

   Nell’esempio seguente, il segmento viene denominato [!DNL "Visits with an order"].

3. Trascina nel segmento la metrica di base utilizzata nell’obiettivo di ottimizzazione.

   Nell’esempio riportato di seguito, utilizziamo il **ordini** , in modo che il tasso di conversione misuri la frazione di visite in cui viene registrato un ordine.

4. In alto a sinistra del contenitore di definizione del segmento, seleziona **[!UICONTROL Includi]** **Visita**.
5. Utilizza la **[!UICONTROL è maggiore di]** e impostare il valore su 0.

   Impostare il valore su 0 significa che questo segmento include le visite in cui la metrica degli ordini è positiva.

6. Fai clic su **[!UICONTROL Salva]**.

![Figura7.png](assets/Figure7.png)

*Figura 7: Filtraggio della definizione del segmento alle visite con un ordine positivo. A seconda della metrica di ottimizzazione dell’attività, è necessario sostituire gli ordini con una metrica appropriata*

**Applicalo alle visite nella metrica filtrata dell’attività**

Questo segmento può ora essere utilizzato per filtrare le visite con un numero positivo di ordini e in cui è stato rilevato un hit per il [!DNL Auto-Target] attività. La procedura di filtraggio di una metrica è simile a prima e dopo l’applicazione del nuovo segmento alla metrica di visita già filtrata, il pannello di rapporto dovrebbe essere simile alla Figura 8

![Figura 8.png](assets/Figure8.png)

*Figura 8: Il pannello di rapporto con la metrica di conversione visita univoca corretta: il numero di visite in cui è stato registrato un hit dall&#39;attività e in cui la metrica di conversione (ordini in questo esempio) era diversa da zero.*

## Passaggio finale: Crea un tasso di conversione che cattura la magia di cui sopra

Con le modifiche apportate al [!UICONTROL Visita] e metriche obiettivo nelle sezioni precedenti, l’ultima modifica da apportare al tuo A4T predefinito per [!DNL Auto-Target] il pannello di reporting è quello di creare tassi di conversione che siano il rapporto corretto, quello della metrica di obiettivo corretta, in una metrica &quot;Visite&quot; filtrata in modo appropriato.

A tale scopo, crea un [!UICONTROL Metrica calcolata] utilizzando i seguenti passaggi:

1. Seleziona la **[!UICONTROL Componenti > Crea metrica]** in [!DNL Analysis Workspace] barra degli strumenti.
1. Specifica una **[!UICONTROL Titolo]** per la metrica. Ad esempio, &quot;Tasso di conversione corretto per le visite per l’attività XXX&quot;.
1. Seleziona **[!UICONTROL Formato]** = percentuale e **[!UICONTROL Luoghi decimali]** = 2.
1. Trascina la metrica di obiettivo pertinente per l’attività (ad esempio, [!UICONTROL Conversioni attività]) nella definizione e utilizza l’icona a forma di ingranaggio su questa metrica di obiettivo per regolare il modello di attribuzione su (Partecipazione|Visita), come descritto in precedenza.
1. Seleziona **[!UICONTROL Aggiungi > Contenitore]** in alto a destra **[!UICONTROL Definizione]** sezione .
1. Selezionare l&#39;operatore di divisione (÷) tra i due contenitori.
1. Trascina il segmento creato in precedenza, denominato &quot;Hit with specifiche (Hit con specifico) [!UICONTROL Targeting automatico] attività&quot; in questa esercitazione per questo specifico [!DNL Auto-Target] attività.
1. Trascina **[!UICONTROL Visite]** nel contenitore di segmenti.
1. Fai clic su **[!UICONTROL Salva]**.

>[!TIP]
>
> Puoi anche creare questa metrica utilizzando la variabile [funzionalità metriche calcolate rapide](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html).

La definizione completa della metrica calcolata è mostrata qui.

![Figura9.png](assets/Figure9.png)

*Figura 7: Definizione della metrica del tasso di conversione del modello corretto per le visite e corretta per l’attribuzione. (Nota che questa metrica dipende dalla metrica e dall’attività dell’obiettivo. In altre parole, questa definizione di metrica non è riutilizzabile tra le attività.)*

>[!IMPORTANT]
>
>La [!UICONTROL Conversione] la metrica del tasso dal pannello A4T non è collegata all’evento di conversione o alla metrica di normalizzazione nella tabella. Quando apporti le modifiche suggerite in questa esercitazione, la [!UICONTROL Conversione] il tasso non si adatta automaticamente ai cambiamenti. Pertanto, se apporti la modifica all’attribuzione dell’evento di conversione o alla metrica di normalizzazione (o a entrambe), devi ricordare come passaggio finale per modificare anche la metrica di [!UICONTROL Conversione] , come illustrato in precedenza.

## Riepilogo: Esempio finale [!DNL Analysis Workspace] pannello per [!UICONTROL Targeting automatico] rapporti

Combinando tutti i passaggi sopra descritti in un unico pannello, la figura seguente mostra una visualizzazione completa del rapporto consigliato per [!UICONTROL Targeting automatico] Attività A4T. Questo rapporto è lo stesso utilizzato dalla [!DNL Target] Modelli ML per ottimizzare la metrica dell’obiettivo. Il rapporto include tutte le sfumature e le raccomandazioni discusse in questa esercitazione. Questo rapporto è anche più vicino alle metodologie di conteggio utilizzate nelle tradizionali [!DNL Target]- basati su rapporti [!UICONTROL Targeting automatico] attività.

Fare clic per espandere l&#39;immagine.

![Rapporto finale A4T in [!DNL Analysis Workspace]](assets/Figure10.png "Rapporto A4T in Analysis Workspace"){width="600" zoomable="yes"}

*Figura 10: L’A4T finale [!UICONTROL Targeting automatico] in [!DNL Adobe Analytics] [!DNL Workspace], che combina tutte le regolazioni alle definizioni metriche descritte nelle sezioni precedenti di questa esercitazione.*
