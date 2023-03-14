---
title: Impostare rapporti A4T in [!DNL Analysis Workspace] per [!UICONTROL Allocazione automatica] Attività
description: Come si configurano i rapporti A4T in [!DNL Analysis Workspace] per ottenere i risultati previsti durante l’esecuzione di [!UICONTROL Allocazione automatica] attività.
role: User
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#beta newtab=true" tooltip="What are Target Beta release features?"
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 0ab5bc8b2ad4b5b32069b022d95d0862ec84e868
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# Configurazione dei rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Allocate] attività

Un [!DNL Auto-Allocate] l’attività identifica un vincitore tra due o più esperienze e, di conseguenza, ridistribuisce automaticamente più traffico per il vincitore, mentre il test continua a essere eseguito e ad apprendere. Il [!UICONTROL Analytics for Target] Integrazione di (A4T) per [!UICONTROL Allocazione automatica] consente di visualizzare i dati di reporting in [!DNL Adobe Analytics], e puoi anche ottimizzare per eventi personalizzati o metriche definite in [!DNL Analytics].

Sebbene le funzionalità di analisi avanzate siano disponibili in [!DNL Adobe Analytics] [!DNL Analysis Workspace], alcune modifiche al valore predefinito **[!UICONTROL Analytics for Target]** sono necessari per interpretare correttamente [!DNL Auto-Allocate] attività, a causa delle sfumature [criteri di ottimizzazione](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

Questo tutorial illustra le modifiche consigliate per l’analisi [!DNL Auto-Allocate] attività in [!DNL Analysis Workspace]. I concetti chiave sono:

* [!UICONTROL Visitor] deve sempre essere utilizzato come metrica di normalizzazione in [!DNL Auto-Allocate] attività.
* Quando la metrica è un valore [!DNL Adobe Analytics] metrica, il numeratore appropriato per il tasso di conversione dipende dal tipo di criteri di ottimizzazione scelti durante l’impostazione dell’attività.
   * Il criterio di ottimizzazione &quot;massimizza tasso di conversione visitatore univoco&quot; ha un tasso di conversione il cui numeratore è un conteggio dei visitatori univoci con un valore positivo della metrica.
   * Il &quot;valore della metrica di ingrandimento per visitatore*&quot; ha un tasso di conversione il cui numeratore è il valore della metrica regolare in [!DNL Adobe Analytics]. Questo viene fornito per impostazione predefinita nella sezione **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace].
* Quando la metrica di ottimizzazione è un valore [!DNL Target] metrica di conversione definita, valore predefinito **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace] gestisce la configurazione del pannello.
* Il [!UICONTROL Affidabilità] numeri visualizzati in [!DNL Analysis Workspace] non riflettono [statistiche più conservative utilizzate da [!UICONTROL Allocazione automatica]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629)e quindi devono essere ignorati. Fai riferimento a questi valori in [!DNL Target] reportistica.

## Creare A4T per [!DNL Auto-Allocate] pannello in [!DNL Analysis Workspace]

Per creare un elemento A4T per [!DNL Auto-Allocate] rapporto inizia con **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace], come illustrato di seguito. Effettua quindi le seguenti selezioni:

1. **[!UICONTROL Esperienza controllo]**: puoi scegliere qualsiasi esperienza.
2. **[!UICONTROL Normalizing Metric]**: Seleziona Visitatori. [!DNL Auto-Allocate] normalizza sempre i tassi di conversione per visitatori univoci.
3. **[!UICONTROL Metriche di successo]**: seleziona la stessa metrica utilizzata durante la creazione dell’attività. Se si trattasse di un [!DNL Target] metrica di conversione definita, seleziona **Conversione attività**. In caso contrario, seleziona [!DNL Adobe Analytics] metrica utilizzata.

![[!UICONTROL Analytics for Target] configurazione del pannello per [!DNL Auto-Allocate] attività.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics for Target] configurazione del pannello per [!DNL Auto-Allocate] attività.*

>[!NOTE]
>
> Si può anche arrivare ad un **[!UICONTROL Analytics for Target]** se fai clic sul collegamento dalla schermata del rapporto in [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversione] metriche o [!DNL Analytics] metriche con criteri di ottimizzazione &quot;Maximize Metric Value Per Visitor&quot; (Massimizza valore metrica per visitatore)

Il pannello A4T predefinito gestisce [!DNL Auto-Allocate] attività in cui la metrica di obiettivo è [!DNL Target] conversione o un [!DNL Analytics] metrica con criterio di ottimizzazione &quot;Maximize Metric Value Per Visitor&quot; (Massimizza valore metrica per visitatore).

Un esempio di questo pannello viene visualizzato per [!UICONTROL Ricavi] metrica, in cui &quot;Massimizza valore metrica per visitatore&quot; è stato selezionato come criterio di ottimizzazione al momento della creazione dell’attività. Come già accennato, [!DNL Auto-Allocate] utilizza calcoli di affidabilità più prudenti rispetto a quelli utilizzati nel **[!UICONTROL Analytics for Target]** pannello. L’Adobe consiglia di rimuovere la metrica di affidabilità, nonché le relative metriche di incremento inferiore e superiore.

![[!UICONTROL Analytics for Target - Rapporto di allocazione automatica] pannello](assets/AAFigure2.png)

*Figura 2: rapporto consigliato per [!DNL Auto-Allocate] attività con un [!DNL Analytics] metrica &quot;Massimizzare il valore della metrica per ottimizzazione visitatore&quot;. Per questi tipi di metriche, nonché [!DNL Target] metriche di conversione definite, l&#39;impostazione predefinita **[!UICONTROL Analytics for Target]**pannello in [!DNL Analysis Workspace] possono essere utilizzati.*

## [!DNL Analytics] metriche con criteri di ottimizzazione &quot;Massimizza tasso di conversione visitatore univoco&quot;

Quando un [!DNL Adobe Analytics] La metrica viene utilizzata con un criterio di ottimizzazione di *Massimizzare il tasso di conversione visita*, il valore predefinito **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace] deve essere modificato.

La metrica di successo è ora un conteggio dei visitatori univoci per i quali la metrica di conversione era positiva. Ciò può essere ottenuto creando un segmento che filtra gli hit con un valore positivo della metrica. Crea questo segmento come segue:

1. Seleziona la **[!UICONTROL Componenti]** > **[!UICONTROL Crea segmento]** opzione in [!DNL Analysis Workspace] barra degli strumenti.
1. Trascina la metrica utilizzata al momento della creazione dell’attività dal pannello di sinistra al **[!UICONTROL Definizione]** del segmento.
1. Seleziona i valori della metrica che sono **maggiore di** valore numerico 0.
1. Dalla sezione **[!UICONTROL Includi]** a discesa, seleziona **[!UICONTROL Visitor]**.
1. Assegna al segmento un nome appropriato.

La figura seguente mostra un esempio di creazione del segmento, dove è possibile selezionare [!UICONTROL Visitatori Con Ricavi Positivi].

![[!UICONTROL Visitatori con ricavi positivi] segmento in [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Creazione di segmenti per [!DNL Adobe Analytics] metriche con criteri di ottimizzazione uguali a &quot;[!UICONTROL Massimizzare il tasso di conversione visita].&quot; In questo esempio, la metrica è [!UICONTROL Ricavi], e l’obiettivo di ottimizzazione è di massimizzare il numero di visitatori con ricavi positivi.*

Dopo aver creato il segmento appropriato, viene  **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace] possono essere modificati.

1. Aggiungi un secondo **Visitatori univoci** metrica accanto al valore esistente [!UICONTROL Visitor] colonna delle metriche.
2. Trascina il segmento appena creato sotto la prima colonna per creare un pannello simile a quello della Figura 4. Nota la differenza: il numero di visitatori univoci con ricavi positivi è una frazione del numero totale di visitatori univoci assegnati a ogni esperienza.

   ![Figura 4.png](assets/AAFigure4.png)

   *Figura 4: Filtraggio [!UICONTROL Visitatori univoci] dal segmento appena creato*

3. Un tasso di conversione può essere [calcolato rapidamente](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) evidenziando la prima e la seconda colonna, facendo clic con il pulsante destro del mouse e selezionando **[!UICONTROL Crea metrica da selezione]** > **[!UICONTROL Dividi]**.

   Il tasso di conversione predefinito deve essere rimosso e sostituito con questa nuova metrica calcolata, come illustrato nell’immagine seguente. Potrebbe essere necessario modificare la metrica calcolata appena creata per visualizzarla come **[!UICONTROL Formato]** > **[!UICONTROL Percentuale]** fino a due cifre decimali, come illustrato.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: La versione finale [!UICONTROL Allocazione automatica] pannello che mostra i tassi di conversione per una metrica di conversione dei ricavi binari*

## Riepilogo

I passaggi descritti in questo tutorial mostrano come configurare correttamente [!DNL Analysis Workspace] da visualizzare [!UICONTROL Allocazione automatica] dati di reporting.

Per riepilogare:

* Quando la metrica è un valore [!DNL Target] una metrica di conversione definita o un [!DNL Adobe Analytics] metrica con criterio di ottimizzazione &quot;Maximize Metric Value Per Visitor&quot; (Massimizza valore metrica per visitatore), deve essere utilizzato il pannello predefinito dell’area di lavoro configurato con i visitatori come metrica di normalizzazione.
* Quando la metrica è un valore [!DNL Adobe Analytics] metrica con criterio di ottimizzazione &quot;Massimizza tasso di conversione visitatore univoco&quot;, devi utilizzare un tasso di conversione definito come la frazione di visitatori per i quali la metrica è positiva. A tal fine, crea un segmento corrispondente che filtra [!UICONTROL Visitatore univoco] metrica.
