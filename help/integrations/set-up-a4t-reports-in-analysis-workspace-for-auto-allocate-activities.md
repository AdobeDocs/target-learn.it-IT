---
title: Impostare rapporti A4T in [!DNL Analysis Workspace] per [!UICONTROL Allocazione automatica] Attività
description: Come si configura [!UICONTROL Analytics for Target] Rapporti di (A4T) in [!DNL Adobe] [!DNL Analysis Workspace] durante l’esecuzione [!UICONTROL Allocazione automatica] attività.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: b22d51d7d231d67af179622755fb4f7ef83474a8
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 0%

---

# Configurazione dei rapporti A4T in [!DNL Analysis Workspace] per le attività di [!DNL Auto-Allocate]

Un [!UICONTROL Allocazione automatica] attività in [!DNL Adobe Target] identifica un vincitore tra due o più esperienze e ridistribuisce automaticamente il traffico del visitatore, mentre il test continua a essere eseguito e ad apprendere. Il [!UICONTROL Analytics for Target] Integrazione di (A4T) per [!UICONTROL Allocazione automatica] consente di visualizzare i dati di reporting in [!DNL Adobe Analytics]e puoi ottimizzare per eventi personalizzati o metriche definite in [!DNL Analytics].

Sebbene le funzionalità di analisi avanzate siano disponibili in [!DNL Adobe Analytics] [!DNL Analysis Workspace], alcune modifiche al valore predefinito [!UICONTROL Analytics for Target] potrebbe essere necessario un pannello per interpretare correttamente [!UICONTROL Allocazione automatica] attività. Queste modifiche sono necessarie a causa delle sfumature [criteri delle metriche di ottimizzazione](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Ogni tipo di metrica di ottimizzazione richiede una configurazione di rapporto diversa in A4T, come segue:

* Utilizzo di un [!DNL Analytics] metrica

   * [!UICONTROL Massimizzare il valore della metrica per visitatore]
   * [!UICONTROL Massimizzare il tasso di conversione visitatore univoco]

* Utilizzo di un [!DNL Target]metrica di conversione definita da

Questo tutorial descrive le linee guida generali di A4T e i passaggi di configurazione dei rapporti specifici per singoli criteri.

## Metriche di Analytics con &quot;[!UICONTROL Massimizzare il valore della metrica per visitatore]&quot; criteri di ottimizzazione

**Definizione**: (valore metrica generale) / ( numero di visitatori)

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | [!DNL Target]Report attivato | Rapporto del pannello A4T |
| --- | --- | --- |
| Massimizzare il valore della metrica per un [!DNL Analytics] metrica | <ul><li>[!UICONTROL Affidabilità] Le metriche di devono essere rimosse.</li><li>[!UICONTROL Lift (Low)] e [!UICONTROL Lift (High)] devono essere rimossi.</li><li>Deseleziona la presentazione della percentuale da [!UICONTROL Tasso di conversione] per evitare confusione. Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li><li>La metrica del tasso di conversione deve essere rinominata &quot;Metrica/Visitatore&quot;.</li></ul> | <ul><li>[!UICONTROL Affidabilità] Le metriche di devono essere rimosse.</li><li>[!UICONTROL Lift (Low)] e [!UICONTROL Lift (High)] devono essere rimossi.</li><li>Deseleziona la presentazione della percentuale da [!UICONTROL Tasso di conversione] per evitare confusione. Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li><li>La metrica del tasso di conversione deve essere rinominata &quot;Metrica/Visitatore&quot;.</li><li>Assicurati che gli intervalli di date e ore siano allineati con i valori visualizzati nell’ [!DNL Target] rapporto. Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li></ul> |

![Massimizzare il valore della metrica per i ricavi](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] metriche con &quot;[!UICONTROL Tasso di conversione visitatore univoco]&quot; criteri di ottimizzazione

**Definizione**: (# di visitatori univoci con un valore positivo della metrica) / (numero totale di visitatori univoci)

Esempio: supponiamo che la metrica di ottimizzazione sia [!UICONTROL Ricavi]. L’attività include cinque visitatori univoci e tre di questi visitatori univoci effettuano un acquisto. In questo esempio, questo valore = (3 visitatori per i quali [!UICONTROL Ricavi] è positivo) / (5 visitatori univoci in totale) = 0,6 = 60%.

>[!NOTE]
>
>Il tasso di conversione a cui si fa riferimento qui può fare riferimento ad azioni al di fuori degli ordini, come clic, impression e così via. In questi casi, il criterio consiste comunque nell’ottimizzare il conteggio dei visitatori che fanno clic rispettivamente su o visualizzano la pagina.

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | Report attivato da Target | Rapporto del pannello A4T |
| --- | --- | --- |
| Massimizzare le conversioni per un [!DNL Analytics] metrica | <ul><li>[!UICONTROL Affidabilità] Le metriche di devono essere rimosse.</li><li>Tutti [!UICONTROL Incremento] Le metriche di devono essere rimosse.</li><li>Deseleziona la presentazione della percentuale da [!UICONTROL Tasso di conversione] per evitare confusione. (Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li></ul> | <ul><li>[!UICONTROL Affidabilità] Le metriche di devono essere rimosse.</li><li>Tutti [!UICONTROL Incremento] Le metriche di devono essere rimosse.</li><li>Crea un segmento per filtrare i visitatori con un valore di metrica positivo che hanno visualizzato l’attività analizzata. Per ulteriori informazioni, consulta [Creare un segmento](#segment) di seguito.</li><li>Sostituisci il popolato automaticamente [!UICONTROL Tasso di conversione] metrica in modo che sia la divisione tra [!UICONTROL Visitatori univoci] con un valore di metrica positivo e visitatori univoci. Per ulteriori informazioni, consulta [Aggiornare la metrica Tasso di conversione](#update-conversion-metric) di seguito.</li><li>Deseleziona la presentazione della percentuale da [!UICONTROL Tasso di conversione] per evitare confusione. Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li><li>Assicurati che gli intervalli di date e ore siano allineati con i valori visualizzati nell’ [!DNL Target] rapporto. Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li></ul> |

### Rapporto predefinito del pannello A4T: indicazioni aggiuntive

Le sezioni seguenti contengono ulteriori informazioni su come impostare il rapporto predefinito del pannello A4T.

#### Crea un segmento {#segment}

1. Fai clic su **Simbolo &quot;+&quot;** accanto a **[!UICONTROL Segmenti]** nella barra a sinistra.

   ![Segno più accanto ai segmenti nella barra a sinistra.](/help/integrations/assets/plus-sign.png)

1. Denomina il segmento &quot;Visitatori con valore della metrica positivo&quot;.
1. Sotto **[!UICONTROL Definizione]**, accanto a **[!UICONTROL Includi]**, seleziona **[!UICONTROL Visitatore]**.
1. Sotto **[!UICONTROL Definizione]**, seleziona la metrica di ottimizzazione nell’attività.

   In questo esempio, supponiamo che [!UICONTROL Ricavi] come metrica di ottimizzazione.

1. Seleziona la &quot;[!UICONTROL è maggiore di]&quot;, quindi specifica &quot;0&quot;.

   Queste impostazioni filtrano per tutti i visitatori con un valore di metrica positivo.

1. Fai clic su **[!UICONTROL Salva]**.

   ![Valore metrico positivo](/help/integrations/assets/positive-metric-value.png)

1. Aggiungi il segmento appena creato denominato &quot;Visitatori con valore metrico positivo&quot; al pannello A4T.
1. Trascina la [!UICONTROL Visitatori univoci] nella stessa colonna del &quot;Visitatori con valore di metrica positivo&quot;.

   Questa configurazione crea un segmento di tutti i visitatori univoci per i quali il valore della metrica è positivo. In questo esempio, tutti i visitatori univoci il cui ricavo era maggiore di zero.

#### Aggiornare il [!UICONTROL Tasso di conversione] metrica {#update-conversion-metric}

1. Se non lo hai già fatto, rimuovi il [!UICONTROL Tasso di conversione] dal pannello, come spiegato di seguito.
1. Per aggiungere una metrica, fai clic sul segno &quot;+&quot; accanto al **[!UICONTROL Metriche]** nella barra a sinistra.
1. Denomina la metrica &quot;Tasso di conversione&quot; e definiscilo come &quot;([!UICONTROL Visitatori univoci] con un valore di metrica positivo)&quot; divisa per &quot;Visitatori univoci&quot;, come illustrato di seguito.

   Aggiungi il segmento appena creato (passaggi definiti di seguito) di &quot;Visitatori con valore metrico positivo&quot;, l’operatore di divisione, la metrica &quot;Visitatori univoci&quot; nel numeratore e &quot;Visitatori univoci&quot; come denominatore.

   ![Tasso di conversione nel pannello A4T.](/help/integrations/assets/conversion-rate.png)

1. Fai clic su **[!UICONTROL Salva]**.

1. Trascina la metrica &quot;Tasso di conversione&quot; appena creata nel pannello esistente.
1. Fai clic sull’icona, quindi deseleziona la **[!UICONTROL Percentuale]** , perché questo valore può causare confusione.

   La corretta configurazione del rapporto dovrebbe produrre un risultato simile a quello dell’illustrazione seguente:

   ![Tasso di conversione visita univoco nel rapporto del pannello A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]Tasso di conversione definito

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | Report attivato da Target | Rapporto del pannello A4T |
| --- | --- | --- |
| [!DNL Analytics] generazione rapporti con [!DNL Target] metrica di conversione | <ul><li>[!UICONTROL Affidabilità] Le metriche di devono essere rimosse.</li><li>[!UICONTROL Lift (Low)] e [!UICONTROL Lift (High)] devono essere rimossi.</li><li>Deseleziona la presentazione della percentuale da [!UICONTROL Tasso di conversione] per evitare confusione. Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li></ul> | <ul><li>[!UICONTROL Affidabilità] Le metriche di devono essere rimosse.</li><li>[!UICONTROL Lift (Low)] e [!UICONTROL Lift (High)] devono essere rimossi.</li><li>Deseleziona la presentazione della percentuale da [!UICONTROL Tasso di conversione] per evitare confusione. Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li><li>Assicurati che gli intervalli di date e ore siano allineati con i valori visualizzati nell’ [!DNL Target] rapporto. Per ulteriori informazioni, consulta [Linee guida generali](#guidance) di seguito.</li></ul> |

La corretta configurazione del rapporto dovrebbe produrre un risultato simile a quello dell’illustrazione seguente:

![Conversioni di attività](/help/integrations/assets/optimized-table.png)

## Linee guida generali per [!UICONTROL Analytics for Target] (A4T) {#guidance}

Puoi passare a una predefinita [!UICONTROL Analytics for Target] facendo clic sul collegamento dalla schermata del rapporto in [!UICONTROL Adobe Target] (più avanti in questa guida ci si riferisce a questo come al &quot;[!DNL Target]-triggered report&quot;). In alternativa, puoi creare il pannello A4T in [!DNL Analytics] (i dettagli sono riportati più avanti in questa sezione).

Le sezioni seguenti specificano quali configurazioni sono necessarie, a seconda dei metodi scelti. Tuttavia, i seguenti passaggi fungono da guida generale:

* Le metriche di affidabilità devono essere rimosse dal pannello A4T indipendentemente dal metodo di creazione del pannello (entrambi descritti di seguito). Fai riferimento a questi valori in [!DNL Target] reportistica. Inoltre, i vincitori delle attività possono essere identificati in [!DNL Target] reportistica. I dettagli sull’identificazione dei vincitori dell’attività si trovano nella sezione [Identificare il vincitore dell&#39;attività](#winner) sezione successiva.
>>
* Per evitare confusione, deseleziona la casella di controllo &quot;[!UICONTROL Percentuale]&quot; presentazione del [!UICONTROL Tasso di conversione] metrica. Per ulteriori informazioni, consulta [Nascondi la percentuale dal [!UICONTROL Tasso di conversione] colonna](#hide-percentage) di seguito.
>>
* Se stai creando un pannello A4T, assicurati che gli intervalli di date e ore corrispondano a quelli del [!DNL Target] rapporto. Per ulteriori informazioni, consulta [Allineare data e ora nel pannello A4T](#aligning-date-and-time) di seguito.

### Nascondi la percentuale dal [!UICONTROL Tasso di conversione] colonna {#hide-percentage}

1. Fai clic su **ingranaggio** accanto al titolo del [!UICONTROL Tasso di conversione] colonna.

   ![Icona ingranaggio nella colonna Tasso di conversione](/help/integrations/assets/coversion-rate-gear-icon.png)

   Il [!UICONTROL Colonna] viene visualizzata la finestra di dialogo delle impostazioni:

   ![Finestra di dialogo Impostazioni colonna](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Deseleziona il **[!UICONTROL Percentuale]** casella di controllo.

   Il pannello A4T ora non include percentuali come tasso di conversione e corrispondenze [!DNL Target], come illustrato di seguito:

   ![La colonna Tasso di conversione non mostra alcuna percentuale](/help/integrations/assets/no-percentages.png)

### Allineare data e ora nel pannello A4T {#aligning-date-and-time}

1. sotto ogni pannello, controlla l’intervallo di date a cui il pannello fa riferimento per assicurarti che l’intervallo di date corrisponda a quello del [!DNL Target] rapporto.

   ![Intervallo di date nel pannello A4T](/help/integrations/assets/date-range.png)

1. In entrata [!DNL Analytics], impostare l&#39;intervallo di tempo su 12:00 - 23:59.

### Identificare il vincitore dell&#39;attività {#winner}

[!DNL Auto-Allocate] i vincitori dell’attività sono selezionati quando è presente un tasso di conversione vincente con valori di affidabilità superiori o pari al 95%. Questi valori devono essere riportati nella [!DNL Target] poiché i calcoli di affidabilità riflettono i metodi più conservativi [!DNL Target] consiglia per [!UICONTROL Allocazione automatica] attività. Per ulteriori informazioni, consulta [Garanzie statistiche di Allocazione automatica](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} nel *[!UICONTROL Guida di Adobe Target per professionisti aziendali]*.

>[!NOTE]
>
I badge &quot;Ancora nessun vincitore&quot; e &quot;Vincitore&quot; non sono disponibili nel pannello A4T in [!DNL Analysis Workspace]. Inoltre, il badge &quot;stella&quot; vincitore visualizzato in [!DNL Target] rapporti per [!UICONTROL Allocazione automatica] le attività devono essere ignorate. Per ulteriori informazioni, consulta [Allocazione automatica](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} in *Supporto A4T per attività di allocazione automatica e targeting automatico* nel *[!UICONTROL Guida di Adobe Target per professionisti aziendali]*.

### Creare A4T per [!UICONTROL Allocazione automatica] pannello in [!DNL Analysis Workspace]

1. Per creare un pannello A4T per un [!UICONTROL Allocazione automatica] rapporto di attività, inizia con [!UICONTROL Analytics for Target] pannello in [!DNL Analysis Workspace], come illustrato di seguito.

   ![Analytics for Target - Rapporto di allocazione automatica](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Effettua le seguenti selezioni:

   * **[!UICONTROL Esperienza controllo]**: scegli un’esperienza.
   * **[!UICONTROL Normalizing Metric]**: Seleziona **[!UICONTROL Visitor]** (incluso nel pannello A4T per impostazione predefinita). [!UICONTROL Allocazione automatica] normalizza sempre i tassi di conversione per visitatori univoci.
   * **Metriche di successo**: seleziona la stessa metrica (ottimizzazione) utilizzata durante la creazione dell’attività. Se si trattasse di un [!DNL Target]metrica di conversione definita da, seleziona **[!UICONTROL Conversione attività]**. In caso contrario, seleziona [!DNL Adobe Analytics] metrica utilizzata.









