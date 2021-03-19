---
title: Come recuperare Recommendations con l’API di consegna
description: Questa parte dell’esercitazione guida gli sviluppatori attraverso i passaggi necessari per recuperare il contenuto dei consigli utilizzando l’API di distribuzione di Adobe Target.
role: Sviluppatori
level: Intermedio
topic: Personalizzazione, Amministrazione, Integrazioni, Sviluppo
feature: API/SDK, Recommendations, amministrazione e configurazione
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: 2c371ea17ce38928bcf3655a0d604a69e29963a0
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---


# Recupero di [!DNL Recommendations] con API di consegna

Le API Adobe Target e Adobe Target [!DNL Recommendations] possono essere utilizzate per fornire risposte alle pagine web, ma possono anche essere utilizzate in esperienze non basate su HTML, incluse app, schermate, console, e-mail, chioschi e altri dispositivi di visualizzazione. In altre parole, quando non è possibile utilizzare le librerie [!DNL Target] e JavaScript, l’ **[!DNL Target]API di consegna** ci consente comunque di accedere all’intera gamma di funzionalità [!DNL Target] per fornire esperienze personalizzate.

>[!NOTE]
>
> Quando richiedi contenuto contenente raccomandazioni effettive (prodotti o elementi consigliati), utilizza l’ [!DNL Target] API di consegna.

Per recuperare i consigli, invia una chiamata Adobe Target Delivery API POST con le informazioni contestuali appropriate, che possono includere un ID utente (da utilizzare con consigli specifici per il profilo, come gli elementi visualizzati di recente dall’utente), un nome mbox pertinente, parametri mbox, parametri di profilo o altri attributi. La risposta includerà entity.ids consigliati (e può includere altri dati di entità) in formato JSON o HTML, che può quindi essere visualizzato nel dispositivo.

L’ [API di consegna](https://developers.adobetarget.com/api/delivery-api/) per Adobe Target espone tutte le funzioni esistenti fornite da una richiesta [!DNL Target] standard.

>[!NOTE]
>API di consegna:
>* Consente di recuperare esperienze o offerte per una posizione e un pubblico in modo RESTful.
>* Non richiede autenticazione.
>* Solo POST.
>* Non elabora i cookie o le chiamate di reindirizzamento.
>* Non richiede o riconosce i &quot;ruoli utente&quot;. Recupera semplicemente il contenuto o segnala gli eventi ai server perimetrali [!DNL Target] .


Per utilizzare l’API di consegna per fornire esperienze [!DNL Target], incluse le raccomandazioni, segui questi passaggi:

1. Crea un’attività [!DNL Target] (A/B, XT, AP o [!DNL Recommendations]) utilizzando il Compositore esperienza basato su moduli (non il Compositore esperienza visivo).
2. Utilizza l’API di consegna per ricevere una risposta per le richieste generate dall’attività [!DNL Target] appena creata.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Creare una raccomandazione utilizzando il Compositore esperienza basato su moduli

Per creare consigli che possono essere utilizzati con l&#39;API di consegna, utilizza il [Compositore basato su moduli](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html).

1. Innanzitutto, crea e salva una progettazione basata su JSON da utilizzare nei consigli. Per un esempio di JSON e informazioni di base su come restituire le risposte JSON durante la configurazione di un’attività basata su moduli, consulta la documentazione su [Creazione di progettazioni di consigli](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html). In questo esempio, la progettazione si chiama *JSON semplice.*

   ![lato server-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. In [!DNL Target], passa a **[!UICONTROL Attività] > [!UICONTROL Crea attività] > [!UICONTROL Recommendations]**, quindi seleziona **[!UICONTROL Modulo]**.

   ![lato server-side-create-recs.png](assets/server-side-create-recs.png)

3. Seleziona una proprietà e fai clic su **[!UICONTROL Avanti]**.
4. Definite la posizione in cui desiderate che gli utenti ricevano la risposta della raccomandazione. L&#39;esempio seguente utilizza una posizione denominata *api_charter*. Seleziona la progettazione basata su JSON, creata in precedenza, denominata *JSON semplice.*
   ![lato server-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Salvate e attivate la raccomandazione. Genererà risultati. [Quando i risultati sono pronti](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), puoi utilizzare l’API di consegna per recuperarli.

## Utilizzare l’API di consegna

La sintassi per [API di consegna](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) è la seguente:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Il codice client è obbligatorio. Come promemoria, il tuo codice client può essere trovato in Adobe Target passando a **[!UICONTROL Recommendations] > [!UICONTROL Impostazioni]**. Nota il valore **[!UICONTROL Codice client]** nella sezione **[!UICONTROL Token API per i consigli]** .
   ![client-code.png](assets/client-code.png)
1. Una volta ottenuto il codice client, crea la chiamata API di consegna. L&#39;esempio seguente inizia con la **[!UICONTROL Chiamata API di consegna delle mbox con batch web]** fornita nella [Raccolta Postman API di consegna](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection), apportando le modifiche necessarie. Ad esempio:
   * gli oggetti **browser** e **address** sono stati rimossi dal **corpo**, in quanto non sono necessari per i casi di utilizzo non HTML
   * *api_* charteris è elencato come nome della posizione in questo esempio
   * entity.id è specificato, poiché questa raccomandazione è basata su Somiglianza del contenuto, che richiede che una chiave di elemento corrente sia passata a [!DNL Target].
      ![server-side-Delivery-API-call.](assets/server-side-delivery-api-call2.png)
pngRicorda di configurare correttamente i parametri di query. Ad esempio, assicurati di specificare 
`{{CLIENT_CODE}}` se necessario. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Invia la richiesta. Questo viene eseguito rispetto alla posizione *api_charter*, che dispone di un consiglio attivo in esecuzione, definita con la progettazione JSON che genera un elenco di entità consigliate.
1. Ricevi una risposta basata sulla progettazione JSON.
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
pngLa risposta include l&#39;ID chiave e gli ID entità delle entità consigliate.

L’utilizzo dell’API di consegna con [!DNL Recommendations] in questo modo consente di eseguire passaggi aggiuntivi prima di visualizzare i consigli al visitatore sul dispositivo non HTML. Ad esempio, puoi prendere la risposta dall’API di consegna per eseguire una ricerca aggiuntiva in tempo reale dei dettagli degli attributi di entità (inventario, prezzo, valutazione e così via) da un altro sistema (ad esempio una piattaforma CMS, PIM o e-commerce) prima di visualizzare i risultati finali.

Utilizzando l’approccio descritto in questa esercitazione, puoi fare in modo che qualsiasi applicazione sfrutti la risposta di [!DNL Target] per fornire consigli personalizzati!

## Implementazioni di esempio

Le risorse seguenti forniscono esempi di diverse implementazioni non basate su HTML. Tieni presente che ogni implementazione sarà unica, a causa del sistema e dei dispositivi interessati.

| Risorsa | Dettagli |
| --- | --- |
| [Utilizzo delle API RESTful in AEM](https://helpx.adobe.com/experience-manager/using/restful-services.html) | Come creare e distribuire un bundle Adobe Experience Manager OSGi che consuma dati da un servizio web RESTful di terze parti. |
| [Adobe Target Ovunque - Implementa il lato server o in IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab che offre un’esperienza pratica per un’applicazione React che sfrutta le API lato server di Adobe Target. |
| [Adobe Target in un’app mobile senza l’SDK per Adobi](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Questa guida illustra come configurare Adobe Target nell’app mobile senza installare l’SDK per Adobe. Questa soluzione utilizza la webview dell’SDK di Tealium e il modulo Comandi remoti per inviare e ricevere richieste all’API visitatore di Adobe (Experience Cloud) e all’API di Adobe Target. |
| [Funzionamento di Adobe Target nelle app per dispositivi mobili](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Funzionamento di [!DNL Target] con l&#39;SDK di Mobile |
| [Configurazione  [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] delle API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Passaggi per configurare l’ estensione [!DNL Target] in Experience Platform Launch, aggiungere l’ [!DNL Target] all’app e implementare le API [!DNL Target] per richiedere attività, preacquisire offerte e accedere alla modalità di anteprima visiva. |
| [Client nodo Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | SDK di Node.js v1.0 open source [!DNL Target] |
| [Panoramica lato server](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Informazioni sulle API di distribuzione lato server di Adobe Target, API di distribuzione in batch lato server, SDK di Node.js e API Adobe Target [!DNL Recommendations]. |
| [Adobe Campaign Content Recommendations in E-mail](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog che descrive come sfruttare i consigli sui contenuti nelle e-mail tramite Adobe Target e Adobe I/O Runtime in Adobe Campaign. |

## Gestione della [!DNL Recommendations] configurazione con le API

Nella maggior parte dei casi, i consigli sono configurati nell’interfaccia utente di Adobe Target, quindi sono utilizzati o accessibili tramite le API [!DNL Target] , per motivi come quelli menzionati nelle sezioni precedenti. Questo coordinamento interfaccia utente-API è comune. Tuttavia, a volte gli utenti possono voler eseguire tutte le azioni tramite API, sia la configurazione che l’utilizzo dei risultati. Anche se molto meno comune, gli utenti possono configurare, eseguire in modo assoluto *e* sfruttare i risultati dei consigli utilizzando interamente le API.

In una [sezione precedente](manage-catalog.md) abbiamo imparato a gestire le entità Recommendations di Adobe Target e a distribuirle lato server. Analogamente, Adobe I/O consente di gestire criteri, promozioni, raccolte e modelli di progettazione senza dover accedere ad Adobe Target. È possibile trovare un elenco completo di tutte le [!DNL Recommendations] API [qui](http://developers.adobetarget.com/api/recommendations/), ma di seguito è riportato un riepilogo di riferimento.

| Risorsa | Dettagli |
| --- | --- |
| [Raccolte](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Elencare, creare, ottenere, modificare ed eliminare le raccolte. |
| [Criteri](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Elenca e ottieni criteri. |
| [Disegni](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Elencare, creare, ottenere, modificare, eliminare e convalidare le progettazioni. |
| [Entità](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Salvare, eliminare e ottenere le entità. |
| [Promozioni](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Elenca, crea, ottieni, modifica ed elimina promozioni. |
| [Criteri di categoria](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Elencare, creare, ottenere, modificare ed eliminare i criteri di categoria. |
| [Criteri personalizzati](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Elencare, creare, ottenere, modificare ed eliminare criteri personalizzati. |
| [Criteri articolo](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Elencare, creare, ottenere, modificare ed eliminare i criteri degli elementi. |
| [Criteri di popolarità](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Elencare, creare, ottenere, modificare ed eliminare i criteri di popolarità. |
| [Criteri degli attributi di profilo](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Elenca, crea, ottieni, modifica ed elimina i criteri degli attributi di profilo. |
| [Criteri recenti](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Elencare, creare, ottenere, modificare ed eliminare criteri recenti. |
| [Criteri di sequenza](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Elencare, creare, ottenere, modificare ed eliminare i criteri di sequenza. |

## Documentazione di riferimento

* [Documentazione API di Adobe Target](https://developers.adobetarget.com/api/#getting-started)
* [API di consegna Adobe Target](https://developers.adobetarget.com/api/delivery-api/)
* [ [!DNL Recommendations] Integrare con l’e-mail](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Riepilogo e revisione

Congratulazioni! Concludendo questa esercitazione hai imparato a:
* [Gestire il catalogo utilizzando l’API di Recommendations](manage-catalog.md)
* [Gestire i criteri personalizzati tramite l’API di Recommendations](manage-custom-criteria.md)
* [Utilizzare l’API di consegna con Recommendations](fetch-recs-server-side-delivery-api.md)
