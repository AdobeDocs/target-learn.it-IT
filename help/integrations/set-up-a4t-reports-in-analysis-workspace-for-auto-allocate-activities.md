---
title: Come impostare i rapporti A4T in [!DNL Analysis Workspace] per [!UICONTROL Allocazione automatica] Attività
description: Come configurare i rapporti A4T in [!DNL Analysis Workspace] per ottenere i risultati previsti durante l'esecuzione [!UICONTROL Allocazione automatica] attività.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: bd8283d3c0e5fa9e690e377bc4dfbf6a147dd577
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Configurazione dei rapporti A4T in [!DNL Analysis Workspace] per [!DNL Auto-Allocate] attività

Un [!DNL Auto-Allocate] l’attività identifica un vincitore tra due o più esperienze e, di conseguenza, ridistribuisce automaticamente più traffico per il vincitore, mentre il test continua a essere eseguito e ad apprendere. La [!UICONTROL Analytics for Target] Integrazione (A4T) per [!UICONTROL Allocazione automatica] consente di visualizzare i dati di reporting in [!DNL Adobe Analytics]e puoi persino ottimizzare eventi personalizzati o metriche definiti in [!DNL Analytics].

Sebbene siano disponibili funzionalità avanzate di analisi in [!DNL Adobe Analytics] [!DNL Analysis Workspace], alcune modifiche all&#39;impostazione predefinita **[!UICONTROL Analytics for Target]** Il pannello è necessario per interpretare correttamente [!DNL Auto-Allocate] attività, a causa delle sfumature [criteri di ottimizzazione](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Questa esercitazione illustra le modifiche consigliate per l&#39;analisi [!DNL Auto-Allocate] attività [!DNL Analysis Workspace]. I concetti chiave sono:

* [!UICONTROL Visitatori] deve essere sempre utilizzato come metrica di normalizzazione in [!DNL Auto-Allocate] attività.
* Quando la metrica è un [!DNL Adobe Analytics] il numeratore appropriato per il tasso di conversione dipende dal tipo di criteri di ottimizzazione scelti durante l’impostazione dell’attività.
   * Il criterio di ottimizzazione &quot;massimizza il tasso di conversione del visitatore univoco&quot; ha un tasso di conversione il cui numeratore è un conteggio dei visitatori unici con un valore positivo della metrica.
   * Il &quot;massimizza il valore della metrica per visitatore&quot; ha un tasso di conversione il cui numeratore è il valore della metrica regolare in [!DNL Adobe Analytics]. Questa è fornita per impostazione predefinita nella **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace].
* Quando la metrica di ottimizzazione è un [!DNL Target] metrica di conversione definita, predefinita **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace] gestisce la configurazione del pannello.
* Per tutti [!UICONTROL Allocazione automatica] attività create prima della [!DNL Target Standard/Premium] Versione 23.3.1 (30 marzo 2023) [!DNL Analytics Workspace] e [!DNL Target] visualizza lo stesso valore per [!UICONTROL Affidabilità].

   Per tutti [!UICONTROL Allocazione automatica] le attività create dopo il 30 marzo 2023, i valori dell’intervallo di affidabilità visualizzati in [!DNL Analysis Workspace] non riflettono [statistiche più conservative utilizzate da [!UICONTROL Allocazione automatica]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} se queste attività *entrambi* delle seguenti condizioni:

   * [!DNL Analytics] come origine per la generazione di rapporti (A4T)
   * [!DNL Analytics] metriche di ottimizzazione

   Se *entrambi* di queste condizioni, le metriche di affidabilità devono essere rimosse dal pannello A4T. Al contrario, fai riferimento a questi valori in [!DNL Target] rapporti.

## Creare A4T per [!DNL Auto-Allocate] pannello in [!DNL Analysis Workspace]

Per creare un A4T per [!DNL Auto-Allocate] inizia con **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace], come illustrato di seguito. Effettua quindi le seguenti selezioni:

1. **[!UICONTROL Control Experience]**: Puoi scegliere qualsiasi esperienza.
2. **[!UICONTROL Normalizzazione della metrica]**: Seleziona Visitatori. [!DNL Auto-Allocate] normalizza sempre i tassi di conversione per visitatori univoci.
3. **[!UICONTROL Metriche di successo]**: Seleziona la stessa metrica utilizzata durante la creazione dell’attività. Se questo fosse un [!DNL Target] metrica di conversione definita, seleziona **Conversione attività**. In caso contrario, seleziona la [!DNL Adobe Analytics] metrica utilizzata.

![[!UICONTROL Analytics for Target] configurazione del pannello per [!DNL Auto-Allocate] attività.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics for Target] configurazione del pannello per [!DNL Auto-Allocate] attività.*

>[!NOTE]
>
> È inoltre possibile ottenere un **[!UICONTROL Analytics for Target]** se fai clic sul collegamento dalla schermata del rapporto in [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversione] metriche o [!DNL Analytics] metriche con criteri di ottimizzazione &quot;Massimizza valore metrica per visitatore&quot;

Maniglie predefinite del pannello A4T [!DNL Auto-Allocate] attività in cui la metrica obiettivo è [!DNL Target] conversione o [!DNL Analytics] con il criterio di ottimizzazione &quot;Massimizza valore metrica per visitatore&quot;.

Viene mostrato un esempio di questo pannello per [!UICONTROL Entrate] , dove &quot;Massimizza valore metrica per visitatore&quot; è stato selezionato come criterio di ottimizzazione al momento della creazione dell’attività. Come accennato in precedenza, [!DNL Auto-Allocate] utilizza calcoli di affidabilità più conservativi rispetto a quelli utilizzati nel **[!UICONTROL Analytics for Target]** pannello. Adobe consiglia di rimuovere la metrica di affidabilità dal pannello A4T, nonché le relative metriche di incremento inferiore e superiore. Fai invece riferimento a questi valori in [!DNL Target] rapporti.

![[!UICONTROL Analytics for Target - Rapporto Allocazione automatica] pannello](assets/AAFigure2.png)

*Figura 2: Rapporto consigliato per [!DNL Auto-Allocate] attività con un [!DNL Analytics] metrica &quot;Massimizza valore metrica per ottimizzazione visitatore&quot; criteri. Per questi tipi di metriche e [!DNL Target] metriche di conversione definite, impostazione predefinita **[!UICONTROL Analytics for Target]**pannello in [!DNL Analysis Workspace] può essere utilizzato.*

## [!DNL Analytics] metriche con i criteri di ottimizzazione &quot;Massimizza tasso di conversione del visitatore univoco&quot;

Quando un [!DNL Adobe Analytics] viene utilizzato con un criterio di ottimizzazione di *Massimizza tasso di conversione del visitatore univoco*, il valore predefinito **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace] devono essere modificati.

La metrica di successo è ora un conteggio di visitatori unici per i quali la metrica di conversione era positiva. Questo può essere ottenuto creando un segmento che filtra gli hit con un valore positivo della metrica. Crea questo segmento come segue:

1. Seleziona la **[!UICONTROL Componenti]** > **[!UICONTROL Crea segmento]** in [!DNL Analysis Workspace] barra degli strumenti.
1. Trascina la metrica utilizzata al momento della creazione dell’attività dal pannello a sinistra al **[!UICONTROL Definizione]** della casella del segmento.
1. Seleziona i valori della metrica che sono **maggiore di** un valore numerico pari a 0.
1. Da **[!UICONTROL Includi]** a discesa, seleziona **[!UICONTROL Visitatori]**.
1. Assegna al segmento un nome appropriato.

Nella figura seguente è illustrato un esempio della creazione del segmento, in cui è possibile selezionare [!UICONTROL Visitatori con ricavi positivi].

![[!UICONTROL Visitatori con ricavi positivi] segmento in [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Creazione di segmenti per [!DNL Adobe Analytics] metriche con criteri di ottimizzazione uguali a &quot;[!UICONTROL Massimizza tasso di conversione del visitatore univoco].&quot; In questo esempio, la metrica è [!UICONTROL Entrate], e l&#39;obiettivo di ottimizzazione è quello di massimizzare il numero di visitatori con ricavi positivi.*

Dopo la creazione del segmento appropriato, l’impostazione predefinita  **[!UICONTROL Analytics for Target]** pannello in [!DNL Analysis Workspace] può essere modificato.

1. Aggiungi un secondo **Visitatori unici** insieme alla metrica esistente [!UICONTROL Visitatori] colonna metrica.
2. Trascina il segmento appena creato sotto la prima colonna per produrre un pannello simile alla Figura 4. Osserva la differenza: il numero di visitatori unici con ricavi positivi è una frazione del numero totale di visitatori univoci assegnati a ogni esperienza.

   ![Figura 4.png](assets/AAFigure4.png)

   *Figura 4: Filtro [!UICONTROL Visitatori unici] dal segmento appena creato*

3. Un tasso di conversione può essere [calcolo rapido](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) evidenziando sia la prima che la seconda colonna, facendo clic con il pulsante destro del mouse e selezionando **[!UICONTROL Crea metrica da selezione]** > **[!UICONTROL Dividi]**.

   Il tasso di conversione predefinito deve essere rimosso e sostituito con questa nuova metrica calcolata, come illustrato nell’immagine seguente. Potrebbe essere necessario modificare la metrica calcolata appena creata per visualizzarla come **[!UICONTROL Formato]** > **[!UICONTROL Percentuale]** fino a due posizioni decimali, come mostrato.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: Il finale [!UICONTROL Allocazione automatica] pannello che mostra i tassi di conversione per una metrica di conversione dei ricavi binarizzata*

## Riepilogo

I passaggi di questa esercitazione hanno dimostrato come configurare correttamente [!DNL Analysis Workspace] per visualizzare [!UICONTROL Allocazione automatica] dati di reporting.

Per riepilogare:

* Quando la metrica è un [!DNL Target] metrica di conversione definita o [!DNL Adobe Analytics] con il criterio di ottimizzazione &quot;Massimizza valore metrica per visitatore&quot;, deve essere utilizzato il pannello dell’area di lavoro predefinito configurato con i visitatori come metrica di normalizzazione.
* Quando la metrica è un [!DNL Adobe Analytics] metrica con criterio di ottimizzazione &quot;Massimizza tasso di conversione del visitatore univoco&quot;, devi utilizzare un tasso di conversione definito come la frazione di visitatori per i quali la metrica è positiva. A questo scopo, crea un segmento corrispondente che filtra i [!UICONTROL Visitatore univoco] metrica.
