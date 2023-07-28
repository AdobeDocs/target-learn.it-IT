---
title: Impostare rapporti A4T in [!DNL Analysis Workspace] per [!UICONTROL Allocazione automatica] Attività
description: Come si configurano i rapporti A4T in [!DNL Analysis Workspace] per ottenere i risultati previsti durante l’esecuzione di [!UICONTROL Allocazione automatica] attività.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 99d49995ec7e3dd502a149376693e2770f3e2a9d
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 0%

---

# Configurazione dei rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Allocate] attività

Un [!DNL Auto-Allocate] l’attività identifica un vincitore tra due o più esperienze e ridistribuisce automaticamente il traffico per il vincitore, mentre il test continua a essere eseguito e ad apprendere. Il [!UICONTROL Analytics for Target] Integrazione di (A4T) per [!UICONTROL Allocazione automatica] consente di visualizzare i dati di reporting in [!DNL Adobe Analytics], e puoi anche ottimizzare per eventi personalizzati o metriche definite in [!DNL Analytics].

Sebbene le funzionalità di analisi avanzate siano disponibili in [!DNL Adobe Analytics] [!DNL Analysis Workspace], alcune modifiche al valore predefinito **[!UICONTROL Analytics for Target]** potrebbe essere necessario un pannello per interpretare correttamente [!DNL Auto-Allocate] attività, a causa delle sfumature [criteri delle metriche di ottimizzazione](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Questo tutorial illustra le modifiche consigliate per l’analisi [!DNL Auto-Allocate] attività in [!DNL Analysis Workspace]. I concetti chiave sono:

* [!UICONTROL Visitor] deve sempre essere utilizzato come metrica di normalizzazione in [!DNL Auto-Allocate] attività.
* Quando la metrica è un valore [!DNL Adobe Analytics] metrica, il calcolo del tasso di conversione varia, a seconda del tipo di criteri di ottimizzazione definiti durante l’impostazione dell’attività.
   * Il numeratore del tasso di conversione &quot;massimizza visitatore univoco&quot; è un conteggio dei visitatori univoci *con un valore positivo della metrica*.
   * Questo metodo non richiede un segmento aggiuntivo per corrispondere al tasso di conversione visualizzato nel [!DNL Target] UI.
* Il numeratore del tasso di conversione &quot;massimizza valore della metrica per visitatore&quot; è il valore della metrica regolare in [!DNL Adobe Analytics]. Questa metrica viene fornita per impostazione predefinita nella [!DNL Analytics for Target] pannello in [!DNL Analysis Workspace].
   * Che cosa significa: massimizza il numero di visitatori che convertono (&quot;conteggia una volta per visitatore&quot;).
   * Questo metodo richiede la creazione di un segmento aggiuntivo nel reporting per corrispondere al tasso di conversione visualizzato nel [!DNL Target] UI.
* Quando la metrica di ottimizzazione è un valore [!DNL Target] metrica di conversione definita, valore predefinito **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace] gestisce la configurazione del pannello.
* Per tutti [!UICONTROL Allocazione automatica] attività create prima del [!DNL Target Standard/Premium] Versione 23.3.1 (30 marzo 2023) [!DNL Analytics Workspace] e [!DNL Target] visualizza lo stesso valore per [!UICONTROL Affidabilità].

  Per tutti [!UICONTROL Allocazione automatica] attività create dopo il 30 marzo 2023, i valori dell’intervallo di affidabilità visualizzati in [!DNL Analysis Workspace] non riflettono [statistiche più conservative utilizzate da [!UICONTROL Allocazione automatica]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} in se tali attività hanno *entrambi* delle seguenti condizioni:

   * [!DNL Analytics] come origine per la generazione di rapporti (A4T)
   * [!DNL Analytics] metriche di ottimizzazione

  Le metriche di affidabilità devono essere rimosse dal pannello A4T. Fai riferimento a questi valori in [!DNL Target] reportistica.

## Creare A4T per [!DNL Auto-Allocate] pannello in [!DNL Analysis Workspace]

Per creare un pannello A4T per un [!DNL Auto-Allocate] rapporto inizia con **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace], come illustrato di seguito. Effettua quindi le seguenti selezioni:

1. **[!UICONTROL Esperienza controllo]**: puoi scegliere qualsiasi esperienza.
1. **[!UICONTROL Normalizing Metric]**: seleziona i visitatori (Visitatori è incluso nel pannello A4T per impostazione predefinita). [!DNL Auto-Allocate] normalizza sempre i tassi di conversione per visitatori univoci.
1. **[!UICONTROL Metriche di successo]**: seleziona la stessa metrica utilizzata durante la creazione dell’attività. Se si trattasse di un [!DNL Target] metrica di conversione definita, seleziona **Conversione attività**. In caso contrario, seleziona [!DNL Adobe Analytics] metrica utilizzata.

![[!UICONTROL Analytics for Target] configurazione del pannello per [!DNL Auto-Allocate] attività.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics for Target] configurazione del pannello per [!DNL Auto-Allocate] attività.*

Si può anche arrivare ad un **[!UICONTROL Analytics for Target]** se fai clic sul collegamento dalla schermata del rapporto in [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversione] metriche o [!DNL Analytics] metriche con criteri di ottimizzazione &quot;Maximize Metric Value Per Visitor&quot; (Massimizza valore metrica per visitatore)

Quando la metrica di obiettivo è:

* Una metrica di conversione di Target
* Metrica di Analytics con criterio di ottimizzazione &quot;Massimizzare il valore della metrica per visitatore&quot;

Il pannello A4T predefinito configura automaticamente il rapporto.

Un esempio di questo pannello viene visualizzato per [!UICONTROL Ricavi] metrica, in cui &quot;Massimizza valore metrica per visitatore&quot; è stato selezionato come criterio di ottimizzazione al momento della creazione dell’attività. Come già accennato, [!DNL Auto-Allocate] utilizza calcoli di affidabilità più prudenti rispetto a quelli utilizzati nel **[!UICONTROL Analytics for Target]** pannello. L’Adobe consiglia di rimuovere la metrica di affidabilità dal pannello A4T, nonché le relative metriche di incremento inferiore e superiore. Fai riferimento invece ai valori di affidabilità in [!DNL Target] reportistica.

>[!NOTE]
>
>I valori di affidabilità nei rapporti di A4T sono meno conservativi di [!DNL Target] e potrebbe indicare in modo prematuro un vincitore per un [!UICONTROL Allocazione automatica] attività.


![[!UICONTROL Analytics for Target - Rapporto di allocazione automatica] pannello](assets/AAFigure2.png)

*Figura 2: rapporto consigliato per [!DNL Auto-Allocate] attività con un [!DNL Analytics] metrica &quot;Massimizzare il valore della metrica per ottimizzazione visitatore&quot;. Per questi tipi di metriche, nonché [!DNL Target] metriche di conversione definite, l&#39;impostazione predefinita **[!UICONTROL Analytics for Target]**pannello in [!DNL Analysis Workspace] possono essere utilizzati.*

## [!DNL Analytics] metriche con criteri di ottimizzazione &quot;Maximize Unique Visitor&quot;

Il criterio di ottimizzazione &quot;Massimizzare visitatore univoco con tasso di conversione&quot; si riferisce al conteggio di visitatori per i quali il valore della metrica è positivo. Ad esempio, se il tasso di conversione è definito come ricavo, il criterio &quot;Massimizza visitatore univoco con tasso di conversione&quot; verrà ottimizzato in base al numero di visitatori univoci per i quali il ricavo è maggiore di 0. In altre parole, questo criterio massimizzerebbe il conteggio dei visitatori che generano ricavi, piuttosto che il valore dei ricavi stessi.

>[!NOTE]
>
>Il tasso di conversione a cui si fa riferimento qui può fare riferimento ad azioni al di fuori degli ordini, come clic, impression e così via. In questi casi, il criterio consiste comunque nell’ottimizzare il conteggio dei visitatori che fanno clic rispettivamente su o visualizzano la pagina.

Il [!DNL Analytics for Target] pannello in [!DNL Analysis Workspace] deve essere modificato se questo criterio di ottimizzazione viene utilizzato con un [!DNL Adobe Analytics] metrica.

Quando si utilizza questo criterio di ottimizzazione, la metrica di successo è un conteggio dei visitatori univoci per i quali la metrica di conversione era positiva. Pertanto, per visualizzare questo valore, è necessario creare un nuovo segmento che filtra gli hit con un valore positivo per la metrica.

Crea questo segmento come segue:

1. Seleziona la **[!UICONTROL Componenti]** > **[!UICONTROL Crea segmento]** opzione in [!DNL Analysis Workspace] barra degli strumenti.
1. Trascina la metrica utilizzata al momento della creazione dell’attività dal pannello di sinistra al **[!UICONTROL Definizione]** del segmento.
1. Seleziona i valori della metrica che sono **maggiore di** valore numerico 0.
1. Dalla sezione **[!UICONTROL Includi]** a discesa, seleziona **[!UICONTROL Visitor]**.
1. Assegna al segmento un nome appropriato.

La figura seguente mostra un esempio di creazione del segmento, dove la metrica di successo è [!UICONTROL Visitatori Con Ricavi Positivi].

![[!UICONTROL Visitatori con ricavi positivi] segmento in [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Creazione di segmenti per [!DNL Adobe Analytics] metriche con criteri di ottimizzazione uguali a &quot;[!UICONTROL Massimizzare il tasso di conversione visita].&quot; In questo esempio, la metrica è [!UICONTROL Ricavi], e l’obiettivo di ottimizzazione è di massimizzare il numero di visitatori con ricavi positivi.*

Dopo aver creato il segmento appropriato, potete modificare il valore predefinito  **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace] per visualizzare i valori dei criteri di ottimizzazione. A tal fine, effettuare le seguenti operazioni:

1. Aggiungi un secondo **Visitatori univoci** metrica accanto al valore esistente [!UICONTROL Visitor] colonna delle metriche.
2. Trascina il segmento appena creato sotto la prima colonna per creare un pannello simile a quello della Figura 4. Nota la differenza nei valori delle colonne: il numero di visitatori univoci con ricavi positivi deve essere una frazione del numero totale di visitatori univoci assegnati a ogni esperienza (come mostrato di seguito).

   ![Figura 4.png](assets/AAFigure4.png)

   *Figura 4: Filtraggio [!UICONTROL Visitatori univoci] dal segmento appena creato*

3. Un tasso di conversione può essere [calcolato rapidamente](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) evidenziando la prima e la seconda colonna, facendo clic con il pulsante destro del mouse e selezionando **[!UICONTROL Crea metrica da selezione]** > **[!UICONTROL Dividi]**.

   Il tasso di conversione predefinito deve essere rimosso e sostituito con questa nuova metrica calcolata, come illustrato nell’immagine seguente. Potrebbe essere necessario modificare la metrica calcolata appena creata per visualizzarla come **[!UICONTROL Formato]** > **[!UICONTROL Percentuale]** fino a due cifre decimali, come illustrato.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: La versione finale [!UICONTROL Allocazione automatica] pannello che mostra i tassi di conversione per una metrica di conversione dei ricavi binari*

## Riepilogo

I passaggi descritti in questo tutorial mostrano come configurare correttamente [!DNL Analysis Workspace] da visualizzare [!UICONTROL Allocazione automatica] dati di reporting.

Per riepilogare:

* Quando la metrica è un valore [!DNL Target] una metrica di conversione definita o un [!DNL Adobe Analytics] metrica con criterio di ottimizzazione &quot;Maximize Metric Value Per Visitor&quot; (Massimizza valore metrica per visitatore), deve essere utilizzato il pannello predefinito dell’area di lavoro configurato con i visitatori come metrica di normalizzazione.
* Quando la metrica è un valore [!DNL Adobe Analytics] metrica con criterio di ottimizzazione &quot;Maximize Unique Visitor Conversion Rate&quot; (Massimizza tasso di conversione visitatore univoco), devi determinare la frazione di visitatori con valore della metrica positivo rispetto al totale dei visitatori. A tal fine, crea un segmento corrispondente che filtra [!UICONTROL Visitatore univoco] su quella metrica.
