---
title: Come impostare rapporti A4T in [!DNL Analysis Workspace]  per [!UICONTROL Auto-Allocate] attività
description: Come si configurano i report [!UICONTROL Analytics for Target] (A4T) in [!DNL Adobe] [!DNL Analysis Workspace] durante l'esecuzione di [!UICONTROL Auto-Allocate] attività.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 190a67832f378e15090115420bfaf8a4af4b9cb9
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 0%

---

# Configurare rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Allocate] attività

Un&#39;attività [[!UICONTROL Auto-Allocate]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html){target=_blank} in [!DNL Adobe Target] identifica un vincitore tra due o più esperienze e ridistribuisce automaticamente il traffico del visitatore al vincitore mentre il test continua a essere eseguito e ad apprendere. L&#39;integrazione di [!UICONTROL Analytics for Target] (A4T) per [!UICONTROL Auto-Allocate] consente di visualizzare i dati di reporting in [!DNL Adobe Analytics] e di ottimizzare eventi o metriche personalizzate definite in [!DNL Analytics].

Sebbene le funzionalità di analisi avanzate siano disponibili in [!DNL Adobe Analytics] [!DNL Analysis Workspace], potrebbero essere necessarie alcune modifiche al pannello predefinito [!UICONTROL Analytics for Target] per interpretare correttamente le attività [!UICONTROL Auto-Allocate]. Queste modifiche sono necessarie a causa delle sfumature presenti in [criteri metrica di ottimizzazione](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Ogni tipo di metrica di ottimizzazione richiede una configurazione di rapporto diversa in A4T, come segue:

* Utilizzo di una metrica [!DNL Analytics]

   * [!UICONTROL Maximize metric value per visitor]
   * [!UICONTROL Maximize unique visitor conversion rate]

* Utilizzo di una metrica di conversione definita da [!DNL Target]

Questo tutorial descrive le linee guida generali di A4T e i passaggi di configurazione dei rapporti specifici per singoli criteri.

## Metriche di Analytics con criteri di ottimizzazione [!UICONTROL Maximize Metric Value Per Visitor]

**Definizione**: (valore metrica generale) / ( numero di visitatori)

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | Report attivato da [!DNL Target] | Rapporto del pannello A4T |
| --- | --- | --- |
| Massimizzare il valore della metrica per una metrica [!DNL Analytics] | <ul><li>Rimuovi [!UICONTROL Confidence] metriche.</li><li>Rimuovi [!UICONTROL Lift (Low)] e [!UICONTROL Lift (High)]. Mantieni [!UICONTROL Lift (Med)].</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Conversion Rate] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li><li>Rinomina la metrica del tasso [!UICONTROL Conversion] in &quot;Metrica/Visitatore&quot;.</li></ul> | <ul><li>Rimuovi [!UICONTROL Confidence] metriche.</li><li>Rimuovi [!UICONTROL Lift (Low)] e [!UICONTROL Lift (High)] Mantieni [!UICONTROL Lift (Med)].</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Conversion Rate] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li><li>Rinomina la metrica del tasso [!UICONTROL Conversion] in &quot;Metrica/Visitatore&quot;.</li><li>Verificare che gli intervalli di date e ore siano allineati ai valori visualizzati nel report [!DNL Target]. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> |

![Massimizzare il valore della metrica per i ricavi](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] metriche con criteri di ottimizzazione &quot;[!UICONTROL Unique Visitor Conversion Rate]&quot;

**Definizione**: (# visitatori univoci con un valore positivo della metrica) / (numero totale di visitatori univoci)

Esempio: supponiamo che la metrica di ottimizzazione sia [!UICONTROL Revenue]. L’attività include cinque visitatori univoci e tre di questi visitatori univoci effettuano un acquisto. In questo esempio, questo valore = (3 visitatori per i quali [!UICONTROL Revenue] è positivo) / (5 visitatori univoci totali) = 0,6 = 60%.

>[!NOTE]
>
>Il tasso di conversione a cui si fa riferimento qui può fare riferimento ad azioni al di fuori degli ordini, come clic, impression e così via. In questi casi, il criterio consiste comunque nell’ottimizzare il conteggio dei visitatori che fanno clic rispettivamente su o visualizzano la pagina.

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | Report attivato da Target | Rapporto del pannello A4T |
| --- | --- | --- |
| Massimizzare le conversioni per una metrica [!DNL Analytics] | <ul><li>Rimuovi [!UICONTROL Confidence] metriche.</li><li>Rimuovi tutte e tre le metriche [!UICONTROL Lift].</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Conversion Rate] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> | <ul><li>Rimuovi [!UICONTROL Confidence] metriche.</li><li>Rimuovi tutte e tre le metriche [!UICONTROL Lift].</li><li>Crea un segmento per filtrare i visitatori con un valore di metrica positivo che hanno visualizzato l’attività analizzata. Vedi [Crea un segmento](#segment) di seguito.</li><li>Sostituire la metrica [!UICONTROL Conversion Rate] con compilazione automatica in modo che sia la divisione tra [!UICONTROL Unique visitors] con un valore di metrica positivo e visitatori univoci. Vedi [Aggiorna la metrica Tasso di conversione](#update-conversion-metric) di seguito.</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Conversion Rate] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li><li>Verificare che gli intervalli di date e ore siano allineati ai valori visualizzati nel report [!DNL Target]. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> |

### Rapporto predefinito del pannello A4T: indicazioni aggiuntive

Le sezioni seguenti contengono ulteriori informazioni su come impostare il rapporto predefinito del pannello A4T.

#### Crea un segmento {#segment}

1. Fai clic sul segno **&quot;+&quot;** accanto a **[!UICONTROL Segments]** nella barra a sinistra.

   ![Segno più accanto ai segmenti nella barra a sinistra.](/help/integrations/assets/plus-sign.png)

1. Denomina il segmento &quot;Visitatori con valore della metrica positivo&quot;.
1. In **[!UICONTROL Definition]**, accanto a **[!UICONTROL Include]**, selezionare **[!UICONTROL Visitor]**.
1. In **[!UICONTROL Definition]**, seleziona la metrica di ottimizzazione nell&#39;attività.

   In questo esempio, si supponga che [!UICONTROL Revenue] sia la metrica di ottimizzazione.

1. Selezionare l&#39;operatore &quot;[!UICONTROL is greater than]&quot;, quindi specificare &quot;0&quot;.

   Queste impostazioni filtrano per tutti i visitatori con un valore di metrica positivo.

1. Fare clic su **[!UICONTROL Save]**.

   ![Valore metrica positivo](/help/integrations/assets/positive-metric-value.png)

1. Aggiungi il segmento appena creato denominato &quot;Visitatori con valore metrico positivo&quot; al pannello A4T.
1. Trascina e rilascia la metrica [!UICONTROL Unique Visitors] nella stessa colonna di &quot;Visitatori con valore di metrica positivo&quot;.

   Questa configurazione crea un segmento di tutti i visitatori univoci per i quali il valore della metrica è positivo. In questo esempio, tutti i visitatori univoci il cui ricavo era maggiore di zero.

#### Aggiorna la metrica [!UICONTROL Conversion Rate] {#update-conversion-metric}

1. Se non lo hai già fatto, rimuovi la colonna [!UICONTROL Conversion Rate] esistente dal pannello, come spiegato di seguito.
1. Aggiungi una metrica facendo clic sul segno &quot;+&quot; accanto alla sezione **[!UICONTROL Metrics]** nella barra a sinistra.
1. Denomina la metrica &quot;Tasso di conversione&quot; e definiscilo come &quot;([!UICONTROL Unique Visitors] con valore di metrica positivo)&quot; diviso per &quot;Visitatori univoci&quot;, come mostrato di seguito.

   Aggiungi il segmento appena creato (passaggi definiti di seguito) di &quot;Visitatori con valore metrico positivo&quot;, l’operatore di divisione, la metrica &quot;Visitatori univoci&quot; nel numeratore e &quot;Visitatori univoci&quot; come denominatore.

   ![Tasso di conversione nel pannello A4T.](/help/integrations/assets/conversion-rate.png)

1. Fare clic su **[!UICONTROL Save]**.

1. Trascina e rilascia la metrica &quot;Tasso di conversione&quot; appena creata nel pannello esistente.
1. Fare clic sull&#39;icona a forma di ingranaggio, quindi deselezionare la casella di controllo **[!UICONTROL Percent]**. Questo valore può creare confusione.

   La corretta configurazione del rapporto dovrebbe produrre un risultato simile a quello dell’illustrazione seguente:

   ![Tasso di conversione visita univoco nel rapporto del pannello A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## Tasso di conversione definito da [!DNL Target]

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | Report attivato da Target | Rapporto del pannello A4T |
| --- | --- | --- |
| Generazione di rapporti [!DNL Analytics] con [!DNL Target] metrica di conversione | <ul><li>Rimuovi [!UICONTROL Confidence] metriche.</li><li>Rimuovi [!UICONTROL Lift (Low)] e [!UICONTROL Lift (High)]. Mantieni incremento (Med).</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Conversion Rate] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> | <ul><li>Rimuovi [!UICONTROL Confidence] metriche.</li><li>Rimuovi [!UICONTROL Lift (Low)] e [!UICONTROL Lift (High)]. Mantieni [!UICONTROL Lift (Med)].</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Conversion Rate] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li><li>Verificare che gli intervalli di date e ore siano allineati ai valori visualizzati nel report [!DNL Target]. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> |

La corretta configurazione del rapporto dovrebbe produrre un risultato simile a quello dell’illustrazione seguente:

![Conversioni attività](/help/integrations/assets/optimized-table.png)

## Linee guida generali per A4T {#guidance}

È possibile passare a un pannello predefinito di [!UICONTROL Analytics for Target] facendo clic sul collegamento dalla schermata del report in [!UICONTROL Target] (in seguito in questa guida verrà indicato come &quot;[!DNL Target]-triggered report&quot;). In alternativa, puoi creare il pannello A4T in [!DNL Analytics] (i dettagli sono riportati più avanti in questa sezione).

Le sezioni seguenti specificano quali configurazioni sono necessarie, a seconda dei metodi scelti. Tuttavia, i seguenti passaggi fungono da guida generale per A4T:

* Rimuovi le metriche di affidabilità dal pannello A4T indipendentemente dal metodo di creazione del pannello (entrambi descritti di seguito). Fare riferimento a questi valori nel reporting di [!DNL Target]. Inoltre, i vincitori delle attività possono essere identificati nel reporting [!DNL Target]. I dettagli sull&#39;identificazione del vincitore dell&#39;attività si trovano nella sezione [Identificare il vincitore dell&#39;attività](#winner) di seguito.
>>
* Per evitare confusione, deselezionare la presentazione &quot;[!UICONTROL Percent]&quot; della metrica [!UICONTROL Conversion Rate]. Vedi [Nascondi la percentuale dalla [!UICONTROL Conversion Rate] colonna](#hide-percentage) di seguito.
>>
* Se stai creando un pannello A4T, assicurati che gli intervalli di date e ore corrispondano a quelli del tuo report [!DNL Target]. Consulta [Allineare data e ora nel pannello A4T](#aligning-date-and-time) di seguito.

### Nascondi la percentuale dalla colonna [!UICONTROL Conversion Rate] {#hide-percentage}

1. Fai clic sull&#39;icona **ingranaggio** accanto al titolo della colonna [!UICONTROL Conversion Rate].

   ![Icona ingranaggio nella colonna Tasso di conversione](/help/integrations/assets/coversion-rate-gear-icon.png)

   Nella finestra di dialogo delle impostazioni di [!UICONTROL Column] viene visualizzato quanto segue:

   ![Finestra di dialogo Impostazioni colonna](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Deselezionare la casella di controllo **[!UICONTROL Percent]**.

   Il pannello A4T ora non include percentuali come [!UICONTROL Conversion Rate] e corrisponde a [!DNL Target], come mostrato di seguito:

   ![La colonna Tasso di conversione non mostra alcuna percentuale](/help/integrations/assets/no-percentages.png)

### Allineare data e ora nel pannello A4T {#aligning-date-and-time}

1. Sotto ogni pannello, controllare l&#39;intervallo di date a cui fa riferimento il pannello per assicurarsi che l&#39;intervallo di date corrisponda a quello del report [!DNL Target].

   ![Intervallo di date nel pannello A4T](/help/integrations/assets/date-range.png)

1. In [!DNL Analytics], impostare l&#39;intervallo di tempo su 12:00 - 23:59.

### Identificare il vincitore dell&#39;attività {#winner}

[!DNL Auto-Allocate] vincitori di attività sono selezionati quando è presente un tasso di conversione vincente con valori di affidabilità superiori o pari al 95%. È necessario fare riferimento a questi valori nei report [!DNL Target], poiché i calcoli di affidabilità riflettono i metodi più conservativi consigliati da [!DNL Target] per le attività [!UICONTROL Auto-Allocate]. Vedi [Garanzie statistiche di Allocazione automatica](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} in *[!UICONTROL Adobe Target Business Practitioner Guide]*.

>[!NOTE]
>
I badge &quot;Ancora nessun vincitore&quot; e &quot;Vincitore&quot; non sono disponibili nel pannello A4T in [!DNL Analysis Workspace]. Inoltre, il badge &quot;stella&quot; vincitore visualizzato nei report [!DNL Target] per le attività [!UICONTROL Auto-Allocate] deve essere ignorato. Consulta [Allocazione automatica](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} in *Supporto A4T per attività di allocazione automatica e targeting automatico* in *[!UICONTROL Adobe Target Business Practitioner Guide]*.

### Crea il pannello A4T per [!UICONTROL Auto-Allocate] in [!DNL Analysis Workspace]

1. Per creare un pannello A4T per un report attività di [!UICONTROL Auto-Allocate], inizia con il pannello [!UICONTROL Analytics for Target] in [!DNL Analysis Workspace], come illustrato di seguito.

   ![Analytics for Target - Rapporto di allocazione automatica](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Effettua le seguenti selezioni:

   * **[!UICONTROL Control Experience]**: scegli un&#39;esperienza qualsiasi.
   * **[!UICONTROL Normalizing Metric]**: seleziona **[!UICONTROL Visitors]** (incluso nel pannello A4T per impostazione predefinita). [!UICONTROL Auto-Allocate] normalizza sempre i tassi di conversione per i visitatori univoci.
   * **Metriche di successo**: seleziona la stessa metrica (di ottimizzazione) utilizzata durante la creazione dell&#39;attività. Se si tratta di una metrica di conversione definita da [!DNL Target], selezionare **[!UICONTROL Activity Conversion]**. In caso contrario, selezionare la metrica [!DNL Adobe Analytics] utilizzata.









