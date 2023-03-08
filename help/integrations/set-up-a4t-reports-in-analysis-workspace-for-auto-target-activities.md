---
title: Impostare rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Target] Attività
description: Come si configurano i rapporti A4T in [!DNL Analysis Workspace] per ottenere i risultati previsti durante l’esecuzione di [!UICONTROL Targeting automatico] attività?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium newtab=true" tooltip="See what's included in Target Premium."
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 14a362214dce9d698c78438c3a47424b59aa4632
workflow-type: tm+mt
source-wordcount: '2253'
ht-degree: 1%

---

# Configurazione dei rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Target] attività

>[!IMPORTANT]
>
>Per [!UICONTROL Targeting automatico] attività, è necessario controllare la generazione rapporti in [!DNL Analytics Workspace] e creare manualmente un pannello A4T.

Il [!UICONTROL Analytics for Target] Integrazione di (A4T) per [!DNL Auto-Target] le attività utilizzano [!DNL Adobe Target] Assembla gli algoritmi di apprendimento automatico (ML) per scegliere l’esperienza migliore per ogni visitatore in base a profilo, comportamento e contesto, il tutto mentre utilizzi un’ [!DNL Adobe Analytics] metrica di obiettivo.

Sebbene le funzionalità di analisi avanzate siano disponibili in [!DNL Adobe Analytics] [!DNL Analysis Workspace], alcune modifiche al valore predefinito **[!UICONTROL Analytics for Target]** sono necessari per interpretare correttamente [!DNL Auto-Target] attività, a causa delle differenze tra le attività di sperimentazione (manuale [!UICONTROL Test A/B] e [!UICONTROL Allocazione automatica]) e attività di personalizzazione ([!UICONTROL [!UICONTROL Targeting automatico]]).

Questo tutorial illustra le modifiche consigliate per l’analisi [!UICONTROL Targeting automatico] attività in [!DNL Analysis Workspace], che si basano sui seguenti concetti chiave:

* Il **[!UICONTROL Controllo e destinazione]** La dimensione può essere utilizzata per distinguere tra [!UICONTROL Controllo] rispetto a quelle fornite da [!UICONTROL Targeting automatico] algoritmo ML del gruppo.
* Le visite devono essere utilizzate come metrica di normalizzazione quando si visualizzano raggruppamenti delle prestazioni a livello di esperienza. Inoltre, [La metodologia di conteggio predefinita di Adobe Analytics potrebbe includere visite in cui l’utente non vede effettivamente il contenuto dell’attività](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics), ma questo comportamento predefinito può essere modificato utilizzando un segmento con ambito appropriato (dettagli di seguito).
* L’attribuzione con ambito di lookback su visita, nota anche come &quot;intervallo di lookback su visita&quot; nel modello di attribuzione prescritto, viene utilizzata da [!DNL Adobe Target] I modelli ML durante le fasi di apprendimento e lo stesso modello di attribuzione (non predefinito) devono essere utilizzati per suddividere la metrica dell’obiettivo.

## Creare A4T per [!UICONTROL Targeting automatico] pannello in [!DNL Analysis Workspace]

Per creare un elemento A4T per [!UICONTROL Targeting automatico] rapporto, inizia con **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace], come mostrato di seguito, o iniziare con una tabella a forma libera. Effettua quindi le seguenti selezioni:

1. **[!UICONTROL Esperienza controllo]**: puoi scegliere qualsiasi esperienza, ma questa scelta verrà ignorata in un secondo momento. Nota che per [!UICONTROL Targeting automatico] attività, l’esperienza di controllo è in realtà una strategia di controllo, che consiste nel: a) Distribuire in modo casuale tra tutte le esperienze, oppure b) Distribuire un’unica esperienza (questa scelta viene effettuata al momento della creazione dell’attività in [!DNL Adobe Target]). Anche se hai scelto (b), il tuo [!UICONTROL Targeting automatico] attività ha designato come controllo un’esperienza specifica. Segui comunque l’approccio descritto in questo tutorial per l’analisi di A4T per [!UICONTROL Targeting automatico] attività.
2. **[!UICONTROL Normalizing Metric]**: Seleziona [!UICONTROL Visite].
3. **[!UICONTROL Metriche di successo]**: anche se puoi selezionare qualsiasi metrica su cui generare il rapporto, in genere dovresti visualizzare i rapporti sulla stessa metrica scelta per l’ottimizzazione durante la creazione dell’attività in [!DNL Target].

   ![[!UICONTROL Analytics for Target] configurazione del pannello per [!UICONTROL Targeting automatico] attività.](assets/Figure1.png)

   *Figura 1: [!UICONTROL Analytics for Target] configurazione del pannello per [!UICONTROL Targeting automatico] attività.*

>[!TIP]
>
>Per impostare [!UICONTROL Analytics for Target] pannello per [!UICONTROL Targeting automatico] attività, scegli un’esperienza di controllo, scegli [!UICONTROL Visite] come metrica di normalizzazione e scegli la stessa metrica di obiettivo scelta per l’ottimizzazione durante [!DNL Target] creazione di attività.

## Utilizza il [!UICONTROL Controllo e destinazione] dimensione per confrontare il [!DNL Target] assemblare il modello ML per il tuo controllo

Il pannello A4T predefinito è progettato per il classico (manuale) [!UICONTROL Test A/B] o [!UICONTROL Allocazione automatica] attività in cui l’obiettivo è quello di confrontare le prestazioni delle singole esperienze rispetto all’esperienza di controllo. In entrata [!UICONTROL Targeting automatico] attività, tuttavia, il confronto di primo ordine deve essere tra il controllo *strategia* e il target *strategia*. In altri termini, la determinazione dell&#39;incremento delle prestazioni complessive del [!UICONTROL Targeting automatico] modello ML completo sulla strategia di controllo).

Per eseguire questo confronto, utilizzare **[!UICONTROL Controllo e destinazione (Analytics for Target)]** dimensione. Trascina per sostituire **[!UICONTROL Esperienze Target]** nel rapporto A4T predefinito.

Questa sostituzione invalida il valore predefinito [!UICONTROL Incremento e affidabilità] sul pannello A4T. Per evitare confusione, puoi rimuovere queste metriche dal pannello predefinito, lasciando il seguente rapporto:

![[!UICONTROL Esperienze per conversione attività] pannello in [!DNL Analysis Workspace]](assets/Figure2.png)

*Figura 2: rapporto di base consigliato per [!DNL Auto-Target] attività. Questo rapporto è stato configurato per confrontare il traffico di destinazione (gestito dal modello ML del gruppo) con il traffico di controllo.*

>[!NOTE]
>
>Attualmente, [!UICONTROL Incremento e affidabilità] numeri non disponibili per [!UICONTROL Controllo e destinazione] dimensioni per i rapporti A4T per [!UICONTROL Targeting automatico]. Fino all&#39;aggiunta del supporto, [!UICONTROL Incremento e affidabilità] può essere calcolato manualmente scaricando il [calcolatore di affidabilità](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Aggiungere suddivisioni delle metriche a livello di esperienza

Per ottenere ulteriori informazioni sulle prestazioni del modello ML del gruppo, puoi esaminare i raggruppamenti a livello di esperienza del **[!UICONTROL Controllo e destinazione]** dimensione. In entrata [!DNL Analysis Workspace], trascina **[!UICONTROL Esperienze Target]** nel rapporto, quindi suddividi separatamente ciascuna dimensione di controllo e di destinazione.

![[!UICONTROL Esperienze per conversione attività] pannello in [!DNL Analysis Workspace]](assets/Figure3.png)

*Figura 3: Suddivisione della dimensione di destinazione per esperienze Target*

Qui viene mostrato un esempio del rapporto risultante.

![[!UICONTROL Esperienze per conversione attività] pannello in [!DNL Analysis Workspace]](assets/Figure4.png)

*Figura 4: uno standard [!UICONTROL Targeting automatico] generare rapporti con raggruppamenti a livello di esperienza. Tieni presente che la metrica dell’obiettivo potrebbe essere diversa e che la strategia di controllo potrebbe avere una singola esperienza.*

>[!TIP]
>
>In entrata [!DNL Analysis Workspace], fai clic sull’icona a forma di ingranaggio per nascondere le percentuali nella [!UICONTROL Tasso di conversione] per mantenere l’attenzione sui tassi di conversione dell’esperienza. I tassi di conversione verranno quindi formattati come decimali, ma interpretati di conseguenza come percentuali.

## Perché&quot;[!UICONTROL Visite]&quot; è la metrica di normalizzazione corretta per [!UICONTROL Targeting automatico] attività

Durante l&#39;analisi di un [!UICONTROL Targeting automatico] attività, scegli sempre [!UICONTROL Visite] come metrica di normalizzazione predefinita. [!UICONTROL Targeting automatico] la personalizzazione seleziona un’esperienza per un visitatore una volta per visita (formalmente, una volta per [!DNL Target] , il che significa che l’esperienza mostrata a un visitatore può cambiare in ogni singola visita. Pertanto, se usa [!UICONTROL Visitatori univoci] come metrica di normalizzazione, il fatto che un singolo utente possa vedere più esperienze (su visite diverse) condurrebbe a confondere i tassi di conversione.

Un semplice esempio dimostra questo punto: considera uno scenario in cui due visitatori entrano in una campagna che ha solo due esperienze. Il primo visitatore visita due volte. Vengono assegnati all’Esperienza A alla prima visita, ma all’Esperienza B alla seconda visita (a causa del loro stato di profilo che cambia durante la seconda visita). Dopo la seconda visita, il visitatore converte effettuando un ordine. La conversione è attribuita all’esperienza mostrata più di recente (Esperienza B). Anche il secondo visitatore visita due volte e viene mostrata l’Esperienza B entrambe le volte, ma non si converte mai.

Confrontiamo i rapporti a livello di visitatore e di visita:

| Esperienza | Visitatori univoci | Visite | Conversioni | Tasso di conversione normalizzato per il visitatore | Tasso di conversione normalizzato per visita |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| Totali | 2 | 4 | 1 | 50% | 25% |

*Tabella 1: Esempio di confronto dei rapporti normalizzati per visitatore e per visita per uno scenario in cui le decisioni sono permanenti per una visita (e non per visitatore, come con i normali test A/B). In questo scenario, le metriche normalizzate per il visitatore sono confuse.*

Come mostrato nella tabella, esiste una chiara incongruenza dei numeri a livello di visitatore. Nonostante il fatto che ci siano due visitatori univoci totali, questa non è una somma dei singoli visitatori univoci per ogni esperienza. Anche se il tasso di conversione a livello di visitatore non è necessariamente sbagliato, quando si confrontano le singole esperienze, i tassi di conversione a livello di visita hanno probabilmente molto più senso. Formalmente, l’unità di analisi (&quot;visite&quot;) è la stessa dell’unità di fedeltà decisionale, il che significa che è possibile aggiungere e confrontare le suddivisioni delle metriche a livello di esperienza.

## Filtra per le visite effettive all’attività

Il [!DNL Adobe Analytics] metodologia di conteggio predefinita per le visite a [!DNL Target] l&#39;attività potrebbe includere visite in cui l&#39;utente non ha interagito con [!DNL Target] attività. Ciò è dovuto al modo in cui [!DNL Target] le assegnazioni delle attività vengono mantenute in [!DNL Analytics] contesto del visitatore. Di conseguenza, il numero di visite al [!DNL Target] L&#39;attività può a volte essere gonfiata, con conseguente depressione dei tassi di conversione.

Se preferisci segnalare le visite in cui l’utente ha effettivamente interagito con il [!UICONTROL Targeting automatico] attività (tramite l’accesso all’attività, un evento di visualizzazione o visita o una conversione), puoi:

1. Crea un segmento specifico che includa gli hit da [!DNL Target] l&#39;attività in questione e
1. Filtra il [!UICONTROL Visite] metrica che utilizza questo segmento.

**Per creare il segmento:**

1. Seleziona la **[!UICONTROL Componenti > Crea segmento]** opzione in [!DNL Analysis Workspace] barra degli strumenti.
2. Specifica un **[!UICONTROL Titolo]** per il segmento. Nell’esempio mostrato di seguito, il segmento è denominato [!DNL "Hit with specific Auto-Target activity"].
3. Trascina **[!UICONTROL Attività Target]** dimensione al segmento **[!UICONTROL Definizione]** sezione.
4. Utilizza il **[!UICONTROL è uguale a]** operatore.
5. Cerca il tuo [!DNL Target] attività.
6. Fai clic sull’icona, quindi seleziona **[!UICONTROL Modello di attribuzione > Istanza]** come illustrato nella figura riportata di seguito.
7. Fai clic su **[!UICONTROL Salva]**.

![Segmento in [!DNL Analysis Workspace]](assets/Figure5.png)

*Figura 5: Utilizzare un segmento come quello mostrato di seguito per filtrare [!UICONTROL Visite] metrica nella A4T per [!UICONTROL Targeting automatico] rapporto*

Una volta creato il segmento, utilizzalo per filtrare il [!UICONTROL Visite] metrica, quindi la [!UICONTROL Visite] metrica include solo le visite in cui l’utente ha interagito con [!DNL Target] attività.

**Per filtrare [!UICONTROL Visite] utilizzando questo segmento:**

1. Trascina il segmento appena creato dalla barra degli strumenti dei componenti e passa il puntatore del mouse sulla base del segmento **[!UICONTROL Visite]** etichetta della metrica fino a un blu **[!UICONTROL Filtra per]** viene visualizzato il prompt.
2. Rilascia il segmento. Il filtro viene applicato a tale metrica.

Il pannello finale viene visualizzato come segue:

![[!UICONTROL Esperienze per conversione attività] pannello in [!DNL Analysis Workspace]](assets/Figure6.png)

*Figura 6: Pannello di reporting con il segmento &quot;Hit con attività di Targeting automatico specifica&quot; applicato al [!UICONTROL Visite] metrica. Questo segmento garantisce che solo le visite in cui un utente ha effettivamente interagito con il [!DNL Target] l&#39;attività in questione è inclusa nella relazione.*

## Allinea l’attribuzione tra l’apprendimento del modello ML e la generazione di metriche obiettivo

L’integrazione di A4T consente [!UICONTROL Targeting automatico] Modello ML da impostare *addestrato* utilizzando gli stessi dati evento di conversione che [!DNL Adobe Analytics] utilizza per *generare rapporti sulle prestazioni*. Tuttavia, esistono alcune ipotesi che devono essere utilizzate per interpretare questi dati durante la formazione dei modelli ML, che differiscono dalle ipotesi predefinite fatte durante la fase di reporting in [!DNL Adobe Analytics].

In particolare, [!DNL Adobe Target] I modelli ML utilizzano un modello di attribuzione con ambito visita. In altre parole, i modelli ML presuppongono che una conversione debba avvenire durante la stessa visita come visualizzazione del contenuto per l’attività, affinché la conversione possa essere &quot;attribuita&quot; alla decisione presa dal modello ML. Questo è necessario per [!DNL Target] garantire una formazione tempestiva dei suoi modelli; [!DNL Target] non può attendere fino a 30 giorni per una conversione (la finestra di attribuzione predefinita per i rapporti in [!DNL Adobe Analytics]) prima di includerla nei dati di formazione dei suoi modelli.

Pertanto, la differenza tra l’attribuzione utilizzata dalla [!DNL Target] I modelli (durante l’apprendimento) rispetto all’attribuzione predefinita utilizzata per l’esecuzione di query sui dati (durante la generazione del rapporto) potrebbero causare discrepanze. Potrebbe anche sembrare che i modelli ML stiano andando male, quando in realtà il problema sta nell’attribuzione.

>[!TIP]
>
>Se i modelli ML si stanno ottimizzando per una metrica attribuita in modo diverso da quella delle metriche visualizzate in un rapporto, le prestazioni dei modelli potrebbero non corrispondere alle attese. Per evitare questa situazione, assicurati che le metriche dell’obiettivo nel rapporto utilizzino la stessa attribuzione utilizzata da [!DNL Target] modelli ML.

Per visualizzare le metriche di obiettivo con la stessa metodologia di attribuzione utilizzata da [!DNL Target] modelli ML, seguire questi passaggi:

1. Passa il puntatore sull’icona a forma di ingranaggio della metrica obiettivo:

   ![gearicon.png](assets/gearicon.png)

1. Dal menu risultante, scorri fino a **[!UICONTROL Impostazioni dati]**.
1. Seleziona **[!UICONTROL Usa modello di attribuzione non predefinito]** (se non già selezionato).

   ![non predefinito attributionmodel.png](assets/non-defaultattributionmodel.png)

1. Clic **[!UICONTROL Modifica]**.
1. Seleziona **[!UICONTROL Modello]**: **[!UICONTROL Partecipazione]**, e **[!UICONTROL Intervallo di lookback]**: **[!UICONTROL Visita]**.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. Fai clic su **[!UICONTROL Applica]**.

Questi passaggi garantiscono che il rapporto attribuisca la metrica di obiettivo alla visualizzazione dell’esperienza, se si è verificato l’evento della metrica di obiettivo *in qualsiasi momento* (&quot;partecipazione&quot;) nella stessa visita in cui è stata mostrata un’esperienza.

## Passaggio finale: crea un tasso di conversione che acquisisca la magia precedente

Con le modifiche apportate al [!UICONTROL Visita] e metriche obiettivo nelle sezioni precedenti, la modifica finale da apportare al tuo A4T predefinito per [!UICONTROL Targeting automatico] il pannello di reporting consiste nel creare tassi di conversione che siano il rapporto corretto (quello di una metrica di obiettivo con la giusta attribuzione), per un filtrato in modo appropriato [!UICONTROL Visite] metrica.

A tale scopo, crea un [!UICONTROL Metrica calcolata] seguendo la procedura descritta di seguito:

1. Seleziona la **[!UICONTROL Componenti > Crea metrica]** opzione in [!DNL Analysis Workspace] barra degli strumenti.
1. Specifica un **[!UICONTROL Titolo]** per la metrica. Ad esempio, &quot;Tasso di conversione corretto per visita per l’attività XXX&quot;.
1. Seleziona **[!UICONTROL Formato]** = percentuale e **[!UICONTROL Cifre decimali]** = 2.
1. Trascina la metrica di obiettivo pertinente per l’attività (ad esempio, [!UICONTROL Conversioni attività]) nella definizione e utilizza l’icona a forma di ingranaggio in questa metrica di obiettivo per regolare il modello di attribuzione su (Partecipazione|Visita), come descritto in precedenza.
1. Seleziona **[!UICONTROL Aggiungi > Contenitore]** in alto a destra **[!UICONTROL Definizione]** sezione.
1. Seleziona l’operatore di divisione (÷) tra i due contenitori.
1. Trascina il segmento creato in precedenza, denominato &quot;Hit con [!UICONTROL Targeting automatico] attività&quot; in questo tutorial per questo [!DNL Auto-Target] attività.
1. Trascina **[!UICONTROL Visite]** metrica nel contenitore di segmenti.
1. Fai clic su **[!UICONTROL Salva]**.

La definizione completa della metrica calcolata è mostrata qui.

![Figura 7.png](assets/Figure7.png)

*Figura 7: Definizione delle metriche del tasso di conversione del modello corretto per visita e corretto per l’attribuzione. (Nota: questa metrica dipende dalla metrica e dall’attività dell’obiettivo. In altre parole, questa definizione di metrica non è riutilizzabile tra le attività.)*

>[!IMPORTANT]
>
>Il [!UICONTROL Conversione] la metrica di tasso dal pannello A4T non è collegata all’evento di conversione o alla metrica di normalizzazione nella tabella. Quando apporti le modifiche suggerite in questa esercitazione, il [!UICONTROL Conversione] non si adatta automaticamente alle modifiche. Pertanto, se apporti la modifica all’attribuzione dell’evento di conversione o alla metrica di normalizzazione (o a entrambe), devi ricordare come passaggio finale per modificare anche la [!UICONTROL Conversione] come mostrato sopra.

## Riepilogo: campione finale [!DNL Analysis Workspace] pannello per [!UICONTROL Targeting automatico] rapporti

Combinando tutti i passaggi precedenti in un unico pannello, la figura seguente mostra una visualizzazione completa del rapporto consigliato per [!UICONTROL Targeting automatico] Attività A4T. Questo rapporto è lo stesso utilizzato dal [!DNL Target] modelli ML per ottimizzare la metrica obiettivo. Il rapporto incorpora tutte le sfumature e i consigli discussi in questa esercitazione. Questo rapporto è anche il più simile alle metodologie di conteggio utilizzate nelle [!DNL Target]-basato su reporting [!UICONTROL Targeting automatico] attività.

Fare clic per espandere l&#39;immagine.

![Rapporto A4T finale in [!DNL Analysis Workspace]](assets/Figure8.png "Rapporto A4T in Analysis Workspace"){width="600" zoomable="yes"}

*Figura 8: A4T finale [!UICONTROL Targeting automatico] rapporto in [!DNL Adobe Analytics] [!DNL Workspace], che combina tutte le regolazioni alle definizioni delle metriche descritte nelle sezioni precedenti di questa esercitazione.*
