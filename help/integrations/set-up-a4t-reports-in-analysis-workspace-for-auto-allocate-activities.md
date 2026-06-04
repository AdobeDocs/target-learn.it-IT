---
title: Come impostare rapporti A4T in [!DNL Analysis Workspace] per [!UICONTROL attività di allocazione automatica]
description: Come si configurano i report [!UICONTROL Analytics for Target] (A4T) in [!DNL Adobe] [!DNL Analysis Workspace] durante l'esecuzione di [!UICONTROL attività Allocazione automatica].
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
TQID: https://experienceleague.adobe.com/5oQMgqqxw2VN-6cb29j4bwEP6VYmGRLXIp5AMJ3WWM4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 1546
ht-degree: 0%

---

# Configurare rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Allocate] attività

Un&#39;attività [[!UICONTROL Allocazione automatica]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=it){target=_blank} in [!DNL Adobe Target] identifica un vincitore tra due o più esperienze e ridistribuisce automaticamente il traffico del visitatore per il vincitore mentre il test continua a essere eseguito e ad apprendere. L&#39;integrazione di [!UICONTROL Analytics for Target] (A4T) per [!UICONTROL Allocazione automatica] consente di visualizzare i dati di reporting in [!DNL Adobe Analytics] e di ottimizzare eventi o metriche personalizzate definite in [!DNL Analytics].

Sebbene le funzionalità di analisi avanzate siano disponibili in [!DNL Adobe Analytics] [!DNL Analysis Workspace], potrebbero essere necessarie alcune modifiche al pannello predefinito [!UICONTROL Analytics for Target] per interpretare correttamente le attività [!UICONTROL Allocazione automatica]. Queste modifiche sono necessarie a causa delle sfumature presenti nei [criteri di metrica di ottimizzazione](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=it#supported){target=_blank}.

Ogni tipo di metrica di ottimizzazione richiede una configurazione di rapporto diversa in A4T, come segue:

* Utilizzo di una metrica [!DNL Analytics]

   * [!UICONTROL Massimizza valore metrica per visitatore]
   * [!UICONTROL Massimizzare il tasso di conversione visitatore univoco]

* Utilizzo di una metrica di conversione definita da [!DNL Target]

Questo tutorial descrive le linee guida generali di A4T e i passaggi di configurazione dei rapporti specifici per singoli criteri.

## Metriche di Analytics con criteri di ottimizzazione &quot;[!UICONTROL Massimizza valore metrica per visitatore]&quot;

**Definizione**: (valore metrica generale) / ( numero di visitatori)

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | Report attivato da [!DNL Target] | Rapporto del pannello A4T |
| --- | --- | --- |
| Massimizzare il valore della metrica per una metrica [!DNL Analytics] | <ul><li>Rimuovi metriche [!UICONTROL Affidabilità].</li><li>Rimuovi [!UICONTROL Incremento (minimo)] e [!UICONTROL Incremento (massimo)]. Mantieni [!UICONTROL Incremento (Med)].</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Tasso di conversione] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li><li>Rinomina la metrica del tasso di conversione [!UICONTROL 1&rbrace; in &quot;Metrica/Visitatore&quot;.]</li></ul> | <ul><li>Rimuovi metriche [!UICONTROL Affidabilità].</li><li>Rimuovi [!UICONTROL Incremento (Basso)] e [!UICONTROL Incremento (Alto)] Mantieni [!UICONTROL Incremento (Med)].</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Tasso di conversione] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li><li>Rinomina la metrica del tasso di conversione [!UICONTROL 1&rbrace; in &quot;Metrica/Visitatore&quot;.]</li><li>Verificare che gli intervalli di date e ore siano allineati ai valori visualizzati nel report [!DNL Target]. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> |

![Massimizzare il valore della metrica per i ricavi](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] metriche con criteri di ottimizzazione &quot;[!UICONTROL Tasso di conversione visitatore univoco]&quot;

**Definizione**: (# visitatori univoci con un valore positivo della metrica) / (numero totale di visitatori univoci)

Esempio: supponiamo che la metrica di ottimizzazione sia [!UICONTROL Ricavi]. L’attività include cinque visitatori univoci e tre di questi visitatori univoci effettuano un acquisto. In questo esempio, questo valore = (3 visitatori per i quali [!UICONTROL Ricavo] è positivo) / (5 visitatori univoci totali) = 0,6 = 60%.

>[!NOTE]
>
>Il tasso di conversione a cui si fa riferimento qui può fare riferimento ad azioni al di fuori degli ordini, come clic, impression e così via. In questi casi, il criterio consiste comunque nell’ottimizzare il conteggio dei visitatori che fanno clic rispettivamente su o visualizzano la pagina.

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | Report attivato da Target | Rapporto del pannello A4T |
| --- | --- | --- |
| Massimizzare le conversioni per una metrica [!DNL Analytics] | <ul><li>Rimuovi metriche [!UICONTROL Affidabilità].</li><li>Rimuovi tutte e tre le metriche [!UICONTROL Incremento].</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Tasso di conversione] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> | <ul><li>Rimuovi metriche [!UICONTROL Affidabilità].</li><li>Rimuovi tutte e tre le metriche [!UICONTROL Incremento].</li><li>Crea un segmento per filtrare i visitatori con un valore di metrica positivo che hanno visualizzato l’attività analizzata. Vedi [Crea un segmento](#segment) di seguito.</li><li>Sostituisci la metrica [!UICONTROL Tasso di conversione] compilata automaticamente in modo che corrisponda alla divisione tra [!UICONTROL Visitatori univoci] con un valore di metrica positivo e visitatori univoci. Vedi [Aggiorna la metrica Tasso di conversione](#update-conversion-metric) di seguito.</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Tasso di conversione] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li><li>Verificare che gli intervalli di date e ore siano allineati ai valori visualizzati nel report [!DNL Target]. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> |

### Rapporto predefinito del pannello A4T: indicazioni aggiuntive

Le sezioni seguenti contengono ulteriori informazioni su come impostare il rapporto predefinito del pannello A4T.

#### Crea un segmento {#segment}

1. Fai clic sul segno **&quot;+&quot;** accanto a **[!UICONTROL Segmenti]** nella barra a sinistra.

   ![Segno più accanto ai segmenti nella barra a sinistra.](/help/integrations/assets/plus-sign.png)

1. Denomina il segmento &quot;Visitatori con valore della metrica positivo&quot;.
1. In **[!UICONTROL Definizione]**, accanto a **[!UICONTROL Includi]**, seleziona **[!UICONTROL Visitatore]**.
1. In **[!UICONTROL Definizione]**, seleziona la metrica di ottimizzazione nell&#39;attività.

   In questo esempio, supponiamo [!UICONTROL Ricavi] come metrica di ottimizzazione.

1. Selezionare l&#39;operatore &quot;[!UICONTROL è maggiore di]&quot;, quindi specificare &quot;0&quot;.

   Queste impostazioni filtrano per tutti i visitatori con un valore di metrica positivo.

1. Fai clic su **[!UICONTROL Salva]**.

   ![Valore metrica positivo](/help/integrations/assets/positive-metric-value.png)

1. Aggiungi il segmento appena creato denominato &quot;Visitatori con valore metrico positivo&quot; al pannello A4T.
1. Trascina e rilascia la metrica [!UICONTROL Visitatori univoci] nella stessa colonna di &quot;Visitatori con valore di metrica positivo&quot;.

   Questa configurazione crea un segmento di tutti i visitatori univoci per i quali il valore della metrica è positivo. In questo esempio, tutti i visitatori univoci il cui ricavo era maggiore di zero.

#### Aggiorna la metrica [!UICONTROL Tasso di conversione] {#update-conversion-metric}

1. Se non lo hai già fatto, rimuovi la colonna [!UICONTROL Tasso di conversione] esistente dal pannello, come spiegato di seguito.
1. Aggiungi una metrica facendo clic sul segno &quot;+&quot; accanto alla sezione **[!UICONTROL Metriche]** nella barra a sinistra.
1. Denomina la metrica &quot;Tasso di conversione&quot; e definiscilo come &quot;([!UICONTROL Visitatori univoci] con valore di metrica positivo)&quot; diviso per &quot;Visitatori univoci&quot;, come mostrato di seguito.

   Aggiungi il segmento appena creato (passaggi definiti di seguito) di &quot;Visitatori con valore metrico positivo&quot;, l’operatore di divisione, la metrica &quot;Visitatori univoci&quot; nel numeratore e &quot;Visitatori univoci&quot; come denominatore.

   ![Tasso di conversione nel pannello A4T.](/help/integrations/assets/conversion-rate.png)

1. Fai clic su **[!UICONTROL Salva]**.

1. Trascina e rilascia la metrica &quot;Tasso di conversione&quot; appena creata nel pannello esistente.
1. Fai clic sull&#39;icona a forma di ingranaggio, quindi deseleziona la casella di controllo **[!UICONTROL Percentuale]**, perché questo valore può causare confusione.

   La corretta configurazione del rapporto dovrebbe produrre un risultato simile a quello dell’illustrazione seguente:

   ![Tasso di conversione visita univoco nel rapporto del pannello A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## Tasso di conversione definito da [!DNL Target]

Per configurare il rapporto, apporta le seguenti modifiche nel rapporto A4T:

| Modifiche richieste | Report attivato da Target | Rapporto del pannello A4T |
| --- | --- | --- |
| Generazione di rapporti [!DNL Analytics] con [!DNL Target] metrica di conversione | <ul><li>Rimuovi metriche [!UICONTROL Affidabilità].</li><li>Rimuovi [!UICONTROL Incremento (minimo)] e [!UICONTROL Incremento (massimo)]. Mantieni incremento (Med).</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Tasso di conversione] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> | <ul><li>Rimuovi metriche [!UICONTROL Affidabilità].</li><li>Rimuovi [!UICONTROL Incremento (minimo)] e [!UICONTROL Incremento (massimo)]. Mantieni [!UICONTROL Incremento (Med)].</li><li>Deselezionare la presentazione della percentuale dalla colonna [!UICONTROL Tasso di conversione] per evitare confusione. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li><li>Verificare che gli intervalli di date e ore siano allineati ai valori visualizzati nel report [!DNL Target]. Consulta [le linee guida generali per A4T](#guidance) di seguito.</li></ul> |

La corretta configurazione del rapporto dovrebbe produrre un risultato simile a quello dell’illustrazione seguente:

![Conversioni attività](/help/integrations/assets/optimized-table.png)

## Linee guida generali per A4T {#guidance}

Puoi passare a un pannello predefinito di [!UICONTROL Analytics for Target] facendo clic sul collegamento dalla schermata del report in [!UICONTROL Target] (verrà indicato più avanti in questa guida come &quot;[!DNL Target]-triggered report&quot;). In alternativa, puoi creare il pannello A4T in [!DNL Analytics] (i dettagli sono riportati più avanti in questa sezione).

Le sezioni seguenti specificano quali configurazioni sono necessarie, a seconda dei metodi scelti. Tuttavia, i seguenti passaggi fungono da guida generale per A4T:

* Rimuovi le metriche di affidabilità dal pannello A4T indipendentemente dal metodo di creazione del pannello (entrambi descritti di seguito). Fare riferimento a questi valori nel reporting di [!DNL Target]. Inoltre, i vincitori delle attività possono essere identificati nel reporting [!DNL Target]. I dettagli sull&#39;identificazione del vincitore dell&#39;attività si trovano nella sezione [Identificare il vincitore dell&#39;attività](#winner) di seguito.
&#x200B;>>
* Per evitare confusione, deselezionare la presentazione &quot;[!UICONTROL Percent]&quot; della metrica [!UICONTROL Tasso di conversione]. Vedi [Nascondi la percentuale dalla [!UICONTROL colonna Tasso di conversione]](#hide-percentage) di seguito.
&#x200B;>>
* Se stai creando un pannello A4T, assicurati che gli intervalli di date e ore corrispondano a quelli del tuo report [!DNL Target]. Consulta [Allineare data e ora nel pannello A4T](#aligning-date-and-time) di seguito.

### Nascondi la percentuale dalla colonna [!UICONTROL Tasso di conversione] {#hide-percentage}

1. Fai clic sull&#39;icona **ingranaggio** accanto al titolo della colonna [!UICONTROL Tasso di conversione].

   ![Icona ingranaggio nella colonna Tasso di conversione](/help/integrations/assets/coversion-rate-gear-icon.png)

   Nella finestra di dialogo delle impostazioni di [!UICONTROL Colonna] viene visualizzato quanto segue:

   ![Finestra di dialogo Impostazioni colonna](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Deseleziona la casella di controllo **[!UICONTROL Percentuale]**.

   Il pannello A4T ora non include percentuali come [!UICONTROL Tasso di conversione] e corrisponde a [!DNL Target], come mostrato di seguito:

   ![La colonna Tasso di conversione non mostra alcuna percentuale](/help/integrations/assets/no-percentages.png)

### Allineare data e ora nel pannello A4T {#aligning-date-and-time}

1. Sotto ogni pannello, controllare l&#39;intervallo di date a cui fa riferimento il pannello per assicurarsi che l&#39;intervallo di date corrisponda a quello del report [!DNL Target].

   ![Intervallo di date nel pannello A4T](/help/integrations/assets/date-range.png)

1. In [!DNL Analytics], impostare l&#39;intervallo di tempo su 12:00am - 11:59pm.

### Identificare il vincitore dell&#39;attività {#winner}

[!DNL Auto-Allocate] vincitori di attività sono selezionati quando è presente un tasso di conversione vincente con valori di affidabilità superiori o pari al 95%. Questi valori devono essere indicati nei report [!DNL Target], poiché i calcoli di affidabilità riflettono i metodi più conservativi [!DNL Target] consigliati per le attività [!UICONTROL Allocazione automatica]. Vedi [Garanzie statistiche di Allocazione automatica](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html?lang=it#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} nella *[!UICONTROL Guida di Adobe Target Business Practitioner]*.

>[!NOTE]
>
>I badge &quot;Ancora nessun vincitore&quot; e &quot;Vincitore&quot; non sono disponibili nel pannello A4T in [!DNL Analysis Workspace]. Inoltre, il badge &quot;stella&quot; vincitore visualizzato nei report [!DNL Target] per le attività [!UICONTROL Allocazione automatica] deve essere ignorato. Consulta [Allocazione automatica](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=it#aa){target=_blank} in *Supporto A4T per attività di allocazione automatica e targeting automatico* nella *[!UICONTROL Guida di Adobe Target Business Practitioner]*.

### Crea il pannello A4T per [!UICONTROL Allocazione automatica] in [!DNL Analysis Workspace]

1. Per creare un pannello A4T per un report attività di [!UICONTROL Allocazione automatica], inizia con il pannello [!UICONTROL Analytics for Target] in [!DNL Analysis Workspace], come illustrato di seguito.

   ![Analytics for Target - Rapporto di allocazione automatica](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Effettua le seguenti selezioni:

   * **[!UICONTROL Esperienza di controllo]**: scegli un&#39;esperienza qualsiasi.
   * **[!UICONTROL Normalizzazione della metrica]**: seleziona **[!UICONTROL Visitatori]** (inclusi nel pannello A4T per impostazione predefinita). [!UICONTROL Allocazione automatica] normalizza sempre i tassi di conversione per i visitatori univoci.
   * **Metriche di successo**: seleziona la stessa metrica (di ottimizzazione) utilizzata durante la creazione dell&#39;attività. Se si tratta di una metrica di conversione definita da [!DNL Target], selezionare **[!UICONTROL Conversione attività]**. In caso contrario, selezionare la metrica [!DNL Adobe Analytics] utilizzata.









