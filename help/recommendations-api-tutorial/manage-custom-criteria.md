---
title: Gestisci criteri personalizzati
keywords: recommendations;adobe recommendations;premium;api;apis
description: ' Adobe Target Recommendations include un set dedicato di API che consentono di gestire il catalogo di prodotti e/o contenuti raccomandabili; gestire gli algoritmi e le campagne di raccomandazione; e distribuite raccomandazioni in oggetti JSON, HTML o XML da visualizzare in Web, dispositivi mobili, e-mail, IOT e altri canali.'
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# Gestisci criteri personalizzati

A volte gli algoritmi forniti da [!DNL Recommendations] non sono in grado di evidenziare particolari elementi che si desidera promuovere. In questa situazione, i criteri personalizzati forniscono un modo per fornire un set specifico di elementi consigliati per un determinato elemento chiave o categoria. Definite la mappatura tra l&#39;elemento chiave o la categoria e gli elementi raccomandati, quindi importate la mappatura come criterio personalizzato. Questo processo è descritto nella [documentazione sui criteri personalizzati](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html). Come indicato in questa documentazione, è possibile creare, modificare ed eliminare criteri personalizzati tramite l&#39;interfaccia utente [!DNL Target]. Tuttavia, [!DNL Target] fornisce anche una serie di API per criteri personalizzati che consentono una gestione più dettagliata dei criteri personalizzati.

>[!IMPORTANT]
>
>Seguite questa guida all&#39;utilizzo per i criteri personalizzati:
>
> Potete eseguire tutte le operazioni (creare, modificare, eliminare) per un determinato criterio personalizzato utilizzando le API oppure eseguire tutte le operazioni (creare, modificare, eliminare) utilizzando l&#39;interfaccia utente. La gestione dei criteri personalizzati tramite una combinazione dell&#39;interfaccia utente e dell&#39;API potrebbe causare conflitti di informazioni o risultati imprevisti. Ad esempio, la creazione di un criterio personalizzato nell’interfaccia utente ma la successiva modifica tramite API non rifletterà gli aggiornamenti nell’interfaccia utente, anche se verrà aggiornato nel backend, come visibile tramite l’API.

## Crea criteri personalizzati

Per creare criteri personalizzati utilizzando l&#39;API [Crea criteri personalizzati](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom), la sintassi è la seguente:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>I criteri personalizzati creati con l&#39;API Create Custom Criteria (Crea criteri personalizzati), come descritto in questo esercizio, verranno visualizzati nell&#39;interfaccia utente, dove persisteranno. Non potrai modificarle o eliminarle dall’interfaccia utente. È possibile modificarle o eliminarle **tramite API**, ma in entrambi i casi continueranno a essere visualizzate nell&#39;interfaccia [!DNL Target]. Per mantenere l&#39;opzione di modifica o eliminazione dall&#39;interfaccia utente, create i criteri personalizzati utilizzando l&#39;interfaccia utente per [la documentazione](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html), invece di utilizzare l&#39;API Create Custom Criteria (Crea criteri personalizzati).

Seguite questa esercitazione solo dopo aver letto l&#39;avviso riportato sopra e sarete a vostro agio nel creare nuovi criteri personalizzati che non potranno essere eliminati dall&#39;interfaccia utente.

1. Verificare `TENANT_ID` e `API_KEY` per **Crea criteri personalizzati** fare riferimento alle variabili di ambiente Postman stabilite in precedenza. Utilizzate l&#39;immagine seguente per il confronto.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Aggiungi il tuo **Body** come **raw** JSON che definisce la posizione del file CSV dei criteri personalizzati. Utilizzate l&#39;esempio fornito nella documentazione di [Create Custom Criteria API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) come modello, fornendo i vostri `environmentId` e altri valori come necessario. Per questo esempio, utilizzeremo LAST_PURCHASED come chiave.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Inviate la richiesta e osservate la risposta, che contiene i dettagli dei criteri personalizzati appena creati.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Per verificare che i criteri personalizzati siano stati creati, andate  Adobe Target a **[!UICONTROL Recommendations] > [!UICONTROL Criteria]** e cercate i criteri per nome oppure utilizzate l&#39;API **List Custom Criteria API** nel passaggio successivo.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

In questo caso, abbiamo un errore. Esaminiamo l&#39;errore esaminando più da vicino i criteri personalizzati, utilizzando l&#39;API **List Custom Criteria API**.

## Elenca criteri personalizzati

Per recuperare un elenco di tutti i criteri personalizzati insieme ai relativi dettagli, utilizzate l&#39;API [List Custom Criteria API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). La sintassi è la seguente:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Verificare `TENANT_ID` e `API_KEY` come prima e inviare la richiesta. Nella risposta, prendete nota dell&#39;ID criteri personalizzato e dei dettagli relativi al messaggio di errore indicato in precedenza.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

In questo caso, l&#39;errore si è verificato perché le informazioni sul server non sono corrette, ovvero [!DNL Target] non è in grado di accedere al file CSV contenente la definizione dei criteri personalizzati. Modifichiamo i criteri personalizzati per correggere questo problema.

## Modifica criteri personalizzati

Per modificare i dettagli di una definizione di criteri personalizzata, utilizzate l&#39; [Edit Custom Criteria API](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom) (Modifica API criteri personalizzati). La sintassi è la seguente:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verificare `TENANT_ID` e `API_KEY` come prima.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Specificate l’ID dei criteri per i criteri personalizzati da modificare.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. Nel Corpo, fornire JSON aggiornato con le informazioni corrette sul server. Per questo passaggio, specificate l&#39;accesso FTP a un server a cui potete accedere.
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Inviate la richiesta e prendete nota della risposta.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Verificate il successo dei criteri personalizzati aggiornati, utilizzando l&#39;API **Get Custom Criteria API**.

## Ottieni criteri personalizzati

Per visualizzare i dettagli dei criteri personalizzati per uno specifico criterio personalizzato, utilizzate l&#39;API [Get Custom Criteria API](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). La sintassi è la seguente:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Specificate l&#39;ID dei criteri personalizzati di cui desiderate ottenere i dettagli. Inviate la richiesta e rivedete la risposta.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Verificare il successo. (Nel nostro caso, verifica che non ci siano ulteriori errori FTP).
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Facoltativo) Verificare che l&#39;aggiornamento rifletta accuratamente nell&#39;interfaccia utente.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Elimina criteri personalizzati

Utilizzando l&#39;ID criteri indicato in precedenza, eliminate i criteri personalizzati utilizzando l&#39; [Delete Custom Criteria API](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom) (Elimina criteri personalizzati). La sintassi è la seguente:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Specificate l&#39;ID criteri del (singolo) criterio personalizzato da eliminare. Fai clic su **Send** (Invia).
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Verificare che i criteri siano stati eliminati utilizzando Get Custom Criteria (Ottieni criteri personalizzati).
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
In questo caso, l&#39;errore 404 previsto indica che non è possibile trovare i criteri eliminati.

>[!NOTE]
>Come promemoria, i criteri non verranno rimossi dall&#39;interfaccia utente [!DNL Target] anche se sono stati eliminati, perché sono stati creati utilizzando l&#39;API Create Custom Criteria (Crea criterio personalizzato).

Congratulazioni! Ora potete creare, elencare, modificare, eliminare e ottenere dettagli sui criteri personalizzati, utilizzando l&#39;API [!DNL Recommendations]. Nella sezione successiva, utilizzerete l&#39;API di consegna [!DNL Target] per recuperare le raccomandazioni.

[&quot;Recupera Recommendations con l&#39;API di distribuzione lato server&quot; >](fetch-recs-server-side-delivery-api.md)
