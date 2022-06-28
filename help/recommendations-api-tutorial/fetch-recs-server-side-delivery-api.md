---
title: Come recuperare Recommendations con l’API di consegna
description: Questa parte dell’esercitazione guida gli sviluppatori attraverso i passaggi necessari per recuperare il contenuto dei consigli utilizzando l’API di distribuzione di Adobe Target.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 553d1208-647f-479d-acc7-d7760469d642
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 1%

---

# Recupero [!DNL Recommendations] con l’API di consegna

Adobe Target e Adobe Target [!DNL Recommendations] Le API possono essere utilizzate per fornire risposte alle pagine web, ma possono anche essere utilizzate in esperienze non basate su HTML, tra cui app, schermate, console, e-mail, chioschi e altri dispositivi di visualizzazione. In altre parole, quando [!DNL Target] le librerie e JavaScript non possono essere utilizzate, **[!DNL Target]API di consegna** consente di accedere a tutte le [!DNL Target] funzionalità per fornire esperienze personalizzate.

>[!NOTE]
>
> Quando richiedi il contenuto contenente raccomandazioni effettive (prodotti o elementi consigliati), utilizza la funzione [!DNL Target] API di consegna.

Per recuperare i consigli, invia una chiamata Adobe Target Delivery API POST con le informazioni contestuali appropriate, che possono includere un ID utente (da utilizzare con consigli specifici per il profilo, come gli elementi visualizzati di recente dall’utente), un nome mbox pertinente, parametri mbox, parametri di profilo o altri attributi. La risposta includerà entity.ids consigliati (e può includere altri dati di entità) in formato JSON o HTML, che può quindi essere visualizzato nel dispositivo.

La [API di consegna](https://developer.adobe.com/target/implement/delivery-api/){target=&quot;_blank&quot;} per Adobe Target espone tutte le funzionalità esistenti che sono standard [!DNL Target] fornisce.

>[!NOTE]
>API di consegna:
>* Consente di recuperare esperienze o offerte per una posizione e un pubblico in modo RESTful.
>* Non richiede autenticazione.
>* Solo POST.
>* Non elabora i cookie o le chiamate di reindirizzamento.
>* Non richiede o riconosce i &quot;ruoli utente&quot;. Recupera semplicemente il contenuto o segnala gli eventi a [!DNL Target] server perimetrali.


Per utilizzare l’API di consegna [!DNL Target] le esperienze, incluse le raccomandazioni, seguono questi passaggi:

1. Crea un [!DNL Target] attività (A/B, XT, AP o [!DNL Recommendations]) utilizzando il Compositore esperienza basato su moduli (non il Compositore esperienza visivo).
2. Utilizza l’API di consegna per ottenere una risposta per le richieste generate da [!DNL Target] attività appena creata.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Creare una raccomandazione utilizzando il Compositore esperienza basato su moduli

Per creare consigli che possono essere utilizzati con l’API di consegna, utilizza il [Compositore basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

1. Innanzitutto, crea e salva una progettazione basata su JSON da utilizzare nei consigli. Per un esempio di JSON e informazioni di base su come restituire le risposte JSON durante la configurazione di un’attività basata su moduli, consulta la documentazione su [Creazione di progettazioni di consigli](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=en). In questo esempio, la progettazione viene denominata *JSON semplice.*

   ![lato server-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. In [!DNL Target], passa a **[!UICONTROL Attività] > [!UICONTROL Crea attività] > [!UICONTROL Recommendations]**, quindi seleziona **[!UICONTROL Modulo]**.

   ![lato server-side-create-recs.png](assets/server-side-create-recs.png)

3. Seleziona una proprietà e fai clic su **[!UICONTROL Successivo]**.
4. Definite la posizione in cui desiderate che gli utenti ricevano la risposta della raccomandazione. Nell&#39;esempio seguente viene utilizzata una posizione denominata *api_charter*. Seleziona la progettazione basata su JSON, creata in precedenza, denominata *JSON semplice.*
   ![lato server-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Salvate e attivate la raccomandazione. Genererà risultati. [Una volta che i risultati sono pronti](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=en), puoi utilizzare l’API di consegna per recuperarle.

## Utilizzare l’API di consegna

La sintassi per [API di consegna](https://developer.adobe.com/target/implement/delivery-api/#tag/Delivery-API){target=&quot;_blank&quot;} è:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Il codice client è obbligatorio. Come promemoria, il tuo codice cliente può essere trovato in Adobe Target navigando in **[!UICONTROL Recommendations] > [!UICONTROL Impostazioni]**. Tieni presente che **[!UICONTROL Codice client]** nel **[!UICONTROL Token API per i consigli]** sezione .
   ![client-code.png](assets/client-code.png)
1. Una volta ottenuto il codice client, crea la chiamata API di consegna. L’esempio seguente inizia con **[!UICONTROL Chiamata API di consegna mbox batch web]** di cui all&quot; [Raccolta Postman API consegna](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)apportare le modifiche necessarie. Ad esempio:
   * la **browser** e **indirizzo** gli oggetti sono stati rimossi dal **Corpo**, poiché non sono necessari per i casi d’uso non HTML
   * *api_charter* è elencato come nome della posizione in questo esempio
   * entity.id è specificato, poiché questa raccomandazione è basata su Somiglianza del contenuto, che richiede il passaggio di una chiave elemento corrente [!DNL Target].
      ![lato server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
Ricorda di configurare correttamente i parametri di query. Ad esempio, assicurati di specificare 
`{{CLIENT_CODE}}` se necessario. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Invia la richiesta. Questo viene eseguito nei confronti del *api_charter* posizione, che dispone di un consiglio attivo in esecuzione, definita con la progettazione JSON che restituisce un elenco di entità consigliate.
1. Ricevi una risposta basata sulla progettazione JSON.
   ![lato server-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
La risposta include l&#39;ID chiave e gli ID entità delle entità consigliate.

Utilizzo dell’API di consegna con [!DNL Recommendations] in questo modo puoi eseguire passaggi aggiuntivi prima di visualizzare consigli al visitatore sul dispositivo non HTML. Ad esempio, puoi prendere la risposta dall’API di consegna per eseguire una ricerca aggiuntiva in tempo reale dei dettagli degli attributi di entità (inventario, prezzo, valutazione e così via) da un altro sistema (ad esempio una piattaforma CMS, PIM o e-commerce) prima di visualizzare i risultati finali.

Utilizzando l’approccio descritto in questa esercitazione, puoi ottenere da qualsiasi applicazione per sfruttare la risposta [!DNL Target] per fornire consigli personalizzati!

## Implementazioni di esempio

Le risorse seguenti forniscono esempi di diverse implementazioni non incentrate su HTML. Tieni presente che ogni implementazione sarà unica, a causa del sistema e dei dispositivi interessati.

| Risorsa | Dettagli |
| --- | --- |
| [Adobe Target Ovunque - Implementa il lato server o in IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab che offre un’esperienza pratica per un’applicazione React che sfrutta le API lato server di Adobe Target. |
| [Adobe Target in un’app mobile senza l’SDK per Adobi](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Questa guida illustra come configurare Adobe Target nell’app mobile senza installare l’SDK per Adobe. Questa soluzione utilizza la webview dell’SDK di Tealium e il modulo Comandi remoti per inviare e ricevere richieste all’API visitatore di Adobe (Experience Cloud) e all’API di Adobe Target. |
| [Funzionamento di Adobe Target nelle app per dispositivi mobili](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html?lang=en) | Come [!DNL Target] funziona con l’SDK di Mobile |
| [Configurazione della [!DNL Target] estensione in Experience Platform Launch e implementazione [!DNL Target] API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Passaggi per la configurazione [!DNL Target] estensione in Experience Platform Launch, aggiunta di [!DNL Target] Estensione all’app e implementazione [!DNL Target] API per richiedere attività, offerte di preacquisizione e modalità di anteprima visiva. |
| [Client nodo Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | Open-source [!DNL Target] SDK di Node.js v1.0 |
| [Panoramica lato server](https://experienceleague.adobe.com/docs/target/using/implement-target/server-side/api-and-sdk-overview.html?lang=en) | Informazioni sulle API di distribuzione lato server di Adobe Target, API di distribuzione in batch lato server, SDK di Node.js e Adobe Target [!DNL Recommendations] API. |
| [Adobe Campaign Content Recommendations in E-mail](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog che descrive come sfruttare i consigli sui contenuti nelle e-mail tramite Adobe Target e Adobe I/O Runtime in Adobe Campaign. |

## Gestione [!DNL Recommendations] Configurazione con le API

Nella maggior parte dei casi, i consigli sono configurati nell’interfaccia utente di Adobe Target e sono quindi utilizzati o accessibili tramite il [!DNL Target] API, per motivi come quelli menzionati nelle sezioni precedenti. Questo coordinamento interfaccia utente-API è comune. Tuttavia, a volte gli utenti possono voler eseguire tutte le azioni tramite API, sia la configurazione che l’utilizzo dei risultati. Anche se molto meno comune, gli utenti possono configurare, eseguire, *e* sfrutta i risultati dei consigli utilizzando interamente le API.

Abbiamo imparato in un [sezione precedente](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=&quot;_blank&quot;} come gestire le entità Adobe Target Recommendations e distribuirle lato server. Analogamente, Adobe I/O consente di gestire criteri, promozioni, raccolte e modelli di progettazione senza dover accedere ad Adobe Target. Un elenco completo di tutti [!DNL Recommendations] È possibile trovare le API [qui](https://developers.adobetarget.com/api/recommendations/), ma ecco un riassunto di riferimento.

| Risorsa | Dettagli |
| --- | --- |
| [Raccolte](https://developers.adobetarget.com/api/recommendations/#tag/Collections) | Elencare, creare, ottenere, modificare ed eliminare le raccolte. |
| [Criteri](https://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Elenca e ottieni criteri. |
| [Progettazioni](https://developers.adobetarget.com/api/recommendations/#tag/Designs) | Elencare, creare, ottenere, modificare, eliminare e convalidare le progettazioni. |
| [Entità](https://developers.adobetarget.com/api/recommendations/#tag/Entities) | Salvare, eliminare e ottenere le entità. |
| [Promozioni](https://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Elenca, crea, ottieni, modifica ed elimina promozioni. |
| [Criteri di categoria](https://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Elencare, creare, ottenere, modificare ed eliminare i criteri di categoria. |
| [Criteri personalizzati](https://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Elencare, creare, ottenere, modificare ed eliminare criteri personalizzati. |
| [Criteri articolo](https://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Elencare, creare, ottenere, modificare ed eliminare i criteri degli elementi. |
| [Criteri di popolarità](https://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Elencare, creare, ottenere, modificare ed eliminare i criteri di popolarità. |
| [Criteri degli attributi di profilo](https://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Elenca, crea, ottieni, modifica ed elimina i criteri degli attributi di profilo. |
| [Criteri recenti](https://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Elencare, creare, ottenere, modificare ed eliminare criteri recenti. |
| [Criteri di sequenza](https://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Elencare, creare, ottenere, modificare ed eliminare i criteri di sequenza. |

## Documentazione di riferimento

* [Documentazione API per l’amministrazione di Adobe Target](https://developer.adobe.com/target/administer/admin-api/){target=&quot;_blank&quot;}
* [API di consegna Adobe Target](https://developer.adobe.com/target/implement/delivery-api/){target=&quot;_blank&quot;}
* [Integrare  [!DNL Recommendations]  con l’e-mail](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Riepilogo e revisione

Congratulazioni! Concludendo questa esercitazione hai imparato a:
* [Gestire il catalogo utilizzando l’API di Recommendations](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=&quot;_blank&quot;}
* [Gestire i criteri personalizzati tramite l’API di Recommendations](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=&quot;_blank&quot;}
* [Utilizzare l’API di consegna con Recommendations](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=&quot;_blank&quot;}
