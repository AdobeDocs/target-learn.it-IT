---
title: Recupero di Recommendations con l'API di distribuzione
keywords: recommendations;adobe recommendations;premium;api;apis
description: ' Adobe Target Recommendations include un set dedicato di API che consentono di gestire il catalogo di prodotti e/o contenuti raccomandabili; gestire gli algoritmi e le campagne di raccomandazione; e distribuite raccomandazioni in oggetti JSON, HTML o XML da visualizzare in Web, dispositivi mobili, e-mail, IOT e altri canali.'
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 18a9b664fe935fd5c52682b2bd798cafd75b6591
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 0%

---


# Recupero [!DNL Recommendations] con l&#39;API di consegna

Le  [!DNL Recommendations] API Adobe Target e  Adobe Target possono essere utilizzate per fornire risposte alle pagine Web, ma possono anche essere utilizzate in esperienze non basate su HTML quali app, schermate, console, e-mail, chioschi e altri dispositivi di visualizzazione. In altre parole, quando [!DNL Target] le librerie e JavaScript non possono essere utilizzati, l&#39;API **[!DNL Target]**di distribuzione ci consente ancora di accedere all&#39;intera gamma di[!DNL Target]funzionalità per fornire esperienze personalizzate.

> [!NOTE]
> Quando richiedete contenuto contenente raccomandazioni effettive (prodotti o elementi consigliati), utilizzate l&#39;API [!DNL Target] di consegna.

Per recuperare le raccomandazioni, inviate una chiamata  Adobe Target Delivery API con le informazioni contestuali appropriate, che può includere un ID utente (da utilizzare con raccomandazioni specifiche del profilo come gli elementi visualizzati di recente dall&#39;utente), un nome mbox pertinente, parametri mbox, parametri di profilo o altri attributi. La risposta includerà entity.ids consigliato (e può includere altri dati di entità) in formato JSON o HTML, che può quindi essere visualizzato nel dispositivo.

L&#39;API [](https://developers.adobetarget.com/api/delivery-api/) di consegna per  Adobe Target espone tutte le funzionalità esistenti fornite da una [!DNL Target] richiesta standard.

>[!NOTE]
>API di consegna:
>* Consente di recuperare esperienze o offerte per una posizione e un pubblico in modo RESTful.
>* Non richiede alcuna autenticazione.
>* Solo POST.
>* Non elabora i cookie o le chiamate di reindirizzamento.
>* Non richiede o riconosce i &quot;ruoli utente&quot;. Recupera semplicemente i contenuti o segnala gli eventi ai server [!DNL Target] periferici.


Per utilizzare l&#39;API di consegna per distribuire [!DNL Target] esperienze, comprese le raccomandazioni, effettuate le seguenti operazioni:

1. Create un&#39; [!DNL Target] attività (A/B, XT, AP o [!DNL Recommendations]) utilizzando Composer basato su modulo (non Visual Experience Composer (Compositore esperienza visivo).
2. Utilizzate l&#39;API Delivery per ottenere una risposta per le richieste generate dall&#39; [!DNL Target] attività appena creata.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Creazione di una raccomandazione tramite Experience Composer basato su modulo

Per creare raccomandazioni che possono essere utilizzate con l&#39;API Delivery, utilizzate Composer basato su [modulo](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html).

1. Innanzitutto, create e salvate una progettazione basata su JSON da utilizzare nella raccomandazione. Per un esempio di JSON, più informazioni di base sulle modalità di restituzione delle risposte JSON durante la configurazione di un&#39;attività basata su moduli, consultate la documentazione sulla [creazione di strutture](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html)di raccomandazione. In questo esempio, la progettazione è denominata JSON *semplice.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. In [!DNL Target], passare a **[!UICONTROL Attività]>[!UICONTROL Crea attività]>[!UICONTROL Recommendations]**, quindi selezionare **[!UICONTROL Modulo]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Selezionate una proprietà e fate clic su **[!UICONTROL Avanti]**.
4. Definite la posizione in cui desiderate che gli utenti ricevano la risposta della raccomandazione. Nell&#39;esempio seguente viene utilizzata una posizione denominata *api_charter*. Selezionate il progetto basato su JSON, creato in precedenza, denominato JSON *semplice.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Salvate e attivate la raccomandazione. Genererà risultati. [Una volta che i risultati sono pronti](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), potete utilizzare l&#39;API di consegna per recuperarli.

## Utilizzare l&#39;API di consegna

The syntax for the [Delivery API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) is:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Il codice client è obbligatorio. Come promemoria, il codice client può essere trovato in  Adobe Target accedendo a **[!UICONTROL Recommendations]>[!UICONTROL Impostazioni]**. Notate il valore del codice **** client nella sezione Token **[!UICONTROL API di]** raccomandazione.
   ![client-code.png](assets/client-code.png)
1. Una volta ottenuto il codice cliente, create la chiamata API di consegna. L&#39;esempio seguente inizia con la chiamata **[!UICONTROL API di consegna delle mbox]** Web Batched fornita nella raccolta [Postman API](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)di consegna, apportando le modifiche necessarie. Ad esempio:
   * gli oggetti **browser** e **indirizzo** sono stati rimossi dal **corpo**, poiché non sono richiesti per i casi di utilizzo non HTML
   * *api_charter* è elencato come nome della posizione in questo esempio
   * entity.id è specificato, poiché questa raccomandazione è basata sulla somiglianza di contenuto, che richiede il passaggio di una chiave di elemento corrente [!DNL Target].
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)Ricorda di configurare correttamente i parametri di query. Ad esempio, accertatevi di specificare`{{CLIENT_CODE}}` come necessario. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Invia la richiesta. Questo viene eseguito rispetto alla posizione *api_charter* , sulla quale è in esecuzione una raccomandazione attiva, definita con la progettazione JSON che genererà un elenco di entità raccomandate.
1. Ricevi una risposta in base alla progettazione JSON.
   ![lato server-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)La risposta include l&#39;ID chiave, nonché gli ID entità delle entità raccomandate.

L&#39;utilizzo dell&#39;API Delivery con [!DNL Recommendations] in questo modo consente di eseguire passaggi aggiuntivi prima di visualizzare le raccomandazioni al visitatore sul dispositivo non HTML. Ad esempio, potete ricevere la risposta dall&#39;API Delivery per eseguire una ricerca aggiuntiva in tempo reale dei dettagli degli attributi di entità (scorte, prezzo, valutazione e così via) da un altro sistema (ad esempio una piattaforma CMS, PIM o e-commerce) prima di visualizzare i risultati finali.

Utilizzando l&#39;approccio descritto in questa esercitazione, potete fare in modo che qualsiasi applicazione sfrutti la risposta da [!DNL Target] per fornire raccomandazioni personalizzate!

## Esempi di implementazioni

Le risorse seguenti forniscono esempi di diverse implementazioni non basate su HTML. Tenere presente che ogni implementazione sarà univoca, a causa del sistema e dei dispositivi coinvolti.

| Risorsa | Dettagli |
| --- | --- |
| [Utilizzo delle API RESTful in AEM](https://helpx.adobe.com/experience-manager/using/restful-services.html) | Come creare e distribuire un bundle Adobe Experience Manager OSGi che consuma i dati provenienti da un servizio Web RESTful di terze parti. |
| [Adobe Target ovunque - Implementa lato server o in IoT](https://expleague.azureedge.net/labs/L733/index.html) |  Adobe Summit 2019 Lab che offre un&#39;esperienza pratica per un&#39;applicazione React che utilizza  API lato server di Adobe Target. |
| [Adobe Target in un&#39;app mobile senza l&#39;SDK del Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Questa guida mostra come impostare  Adobe Target nell’app mobile senza installare l’SDK del Adobe . Questa soluzione utilizza la visualizzazione Web dell’SDK di Tealium e il modulo Comandi remoti per inviare e ricevere richieste all’API del visitatore  Adobe (Experience Cloud ) e all’API Adobe Target . |
| [Come  Adobe Target funziona nelle app mobili](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Come [!DNL Target] funziona con Mobile SDK |
| [Configurazione [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] delle API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Passaggi per configurare l&#39; [!DNL Target] estensione nel Experience Platform Launch, aggiungere l&#39; [!DNL Target] estensione all&#39;app e implementare [!DNL Target] le API per richiedere attività, preacquisire offerte e immettere la modalità di anteprima visiva. |
| [client nodo Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | Node.js SDK open-source [!DNL Target] v1.0 |
| [Panoramica lato server](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Informazioni  API di consegna lato server Adobe Target, API di consegna batch lato server, SDK Node.js e  [!DNL Recommendations] API Adobe Target. |
| [Adobe Campaign Content Recommendations nell&#39;e-mail](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog che descrive come sfruttare le raccomandazioni di contenuto nelle e-mail tramite  Adobe Target e Adobe I/O Runtime in  Adobe Campaign. |

## Gestione dell’ [!DNL Recommendations] impostazione con le API

Nella maggior parte dei casi, le raccomandazioni sono configurate nell&#39;interfaccia  di Adobe Target, quindi utilizzate o accessibili tramite le [!DNL Target] API, per motivi come quelli indicati nelle sezioni precedenti. Questa coordinazione interfaccia utente-API è comune. Tuttavia, a volte gli utenti potrebbero desiderare eseguire tutte le azioni tramite le API, sia la configurazione che l&#39;utilizzo dei risultati. Anche se molto meno comuni, gli utenti possono configurare, eseguire ** e sfruttare appieno i risultati delle raccomandazioni utilizzando interamente le API.

In una sezione [](manage-catalog.md) precedente abbiamo imparato come gestire  entità Adobe Target Recommendations e distribuirle sul lato server. Analogamente,  I/O Adobe consente di gestire criteri, promozioni, raccolte e modelli di progettazione senza dover accedere a  Adobe Target. Un elenco completo di tutte [!DNL Recommendations] le API può essere trovato [qui](http://developers.adobetarget.com/api/recommendations/), ma di seguito è riportato un riepilogo per riferimento.

| Risorsa | Dettagli |
| --- | --- |
| [Raccolte](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Elenca, crea, ottiene, modifica ed elimina le raccolte. |
| [Criteri](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Elenca e ottieni criteri. |
| [Progettazione](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Elenca, crea, ottiene, modifica, elimina e convalida le progettazioni. |
| [Entità](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Salvare, eliminare e ottenere entità. |
| [Promozioni](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Potete elencare, creare, ottenere, modificare ed eliminare le promozioni. |
| [Criteri categoria](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Elenca, crea, ottiene, modifica ed elimina i criteri di categoria. |
| [Criteri personalizzati](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Elenca, crea, ottiene, modifica ed elimina criteri personalizzati. |
| [Criteri articolo](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Elenca, crea, ottiene, modifica ed elimina i criteri degli elementi. |
| [Criteri di popolarità](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Elenca, crea, ottiene, modifica ed elimina i criteri di popolarità. |
| [Criteri attributi profilo](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Elenca, crea, ottiene, modifica ed elimina i criteri degli attributi di profilo. |
| [Criteri recenti](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Elenca, crea, ottiene, modifica ed elimina criteri recenti. |
| [Criteri sequenza](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Elenca, crea, ottiene, modifica ed elimina i criteri di sequenza. |

## Documentazione di riferimento

* [documentazione API Adobe Target](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target Delivery API](https://developers.adobetarget.com/api/delivery-api/)
* [ [!DNL Recommendations] Integrate con e-mail](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Riepilogo e revisione

Congratulazioni! Con questa esercitazione hai imparato a:
* [Gestire il catalogo utilizzando l&#39;API Recommendations](manage-catalog.md)
* [Gestire criteri personalizzati utilizzando l&#39;API Recommendations](manage-custom-criteria.md)
* [Utilizzo dell&#39;API di consegna con Recommendations](fetch-recs-server-side-delivery-api.md)
