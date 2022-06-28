---
title: Come gestire i criteri personalizzati
description: Questa parte dell’esercitazione guida gli sviluppatori attraverso i passaggi necessari per utilizzare le API di Adobe Target per gestire, creare, elencare, modificare, ottenere ed eliminare i criteri di Adobe Target Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: ee63bd3e-200a-4c08-b364-9f17a479033b
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 1%

---

# Gestire criteri personalizzati

A volte gli algoritmi forniti da [!DNL Recommendations] non sono in grado di far emergere particolari articoli che si desidera promuovere. In questa situazione, i criteri personalizzati ti consentono di fornire un set specifico di elementi consigliati per un determinato elemento chiave o categoria. Puoi definire la mappatura tra l’elemento o la categoria chiave e gli elementi consigliati e importarla come criterio personalizzato. Questo processo è descritto in [documentazione sui criteri personalizzati](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en). Come indicato in tale documentazione, puoi creare, modificare ed eliminare criteri personalizzati tramite la funzione [!DNL Target] interfaccia utente (interfaccia utente). Tuttavia, [!DNL Target] fornisce anche un set di API per criteri personalizzati che consentono una gestione più dettagliata dei criteri personalizzati.

>[!IMPORTANT]
>
>Segui questa linea guida di utilizzo per i criteri personalizzati:
>
> Puoi eseguire tutte le operazioni (creare, modificare, eliminare) per un dato criterio personalizzato utilizzando le API oppure fare tutto (creare, modificare, eliminare) utilizzando l’interfaccia utente. La gestione dei criteri personalizzati tramite una combinazione dell’interfaccia utente e dell’API può causare conflitti tra informazioni o risultati imprevisti. Ad esempio, la creazione di un criterio personalizzato nell’interfaccia utente ma la modifica tramite API non rifletterà gli aggiornamenti nell’interfaccia utente, anche se verrà aggiornato nel backend, come visibile tramite l’API.

## Creare criteri personalizzati

Per creare criteri personalizzati utilizzando la variabile [Creare un’API per criteri personalizzati](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom), la sintassi è:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>I criteri personalizzati creati utilizzando l’API Crea criterio personalizzato, come descritto in questo esercizio, verranno visualizzati nell’interfaccia utente, dove persisteranno. Non potrai modificarli o eliminarli dall’interfaccia utente. È possibile modificarli o eliminarli **tramite API**, ma in entrambi i casi, continueranno a essere visualizzati nella [!DNL Target] Interfaccia utente. Per mantenere l’opzione di modifica o eliminazione dall’interfaccia utente, crea i criteri personalizzati utilizzando l’interfaccia utente di per [la documentazione](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en), anziché utilizzare l’API Crea criterio personalizzato.

Procedi con questa esercitazione solo dopo aver letto l’avviso riportato sopra e aver acquisito familiarità con la creazione di nuovi criteri personalizzati che non possono essere successivamente eliminati dall’interfaccia utente.

1. Verifica `TENANT_ID` e `API_KEY` per **Creare criteri personalizzati** fai riferimento alle variabili di ambiente Postman stabilite in precedenza. Usa l&#39;immagine seguente per un confronto.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Aggiungi il tuo **Corpo** come **grezzo** JSON che definisce la posizione del file CSV dei criteri personalizzati. Utilizza l’esempio fornito in [Creare un’API per criteri personalizzati](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) documentazione come modello, fornendo `environmentId` e altri valori, se necessario. Per questo esempio, utilizziamo LAST_PURCHASED come chiave.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Invia la richiesta e osserva la risposta, che contiene i dettagli dei criteri personalizzati appena creati.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Per verificare che i criteri personalizzati siano stati creati, passa all’interno di Adobe Target per **[!UICONTROL Recommendations] > [!UICONTROL Criteri]** e cerca i criteri per nome, oppure utilizza il **API per criteri personalizzati elenco** nel passaggio successivo.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

In questo caso, abbiamo un errore. Esaminiamo l’errore esaminando più da vicino i criteri personalizzati, utilizzando **API per criteri personalizzati elenco**.

## Elenca criteri personalizzati

Per recuperare un elenco di tutti i criteri personalizzati e i relativi dettagli, utilizza la [API per criteri personalizzati elenco](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). La sintassi è la seguente:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Verifica `TENANT_ID` e `API_KEY` come prima, e invia la richiesta. Nella risposta, prendi nota dell’ID criterio personalizzato e dei dettagli relativi al messaggio di errore indicato in precedenza.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

In questo caso, l&#39;errore si è verificato perché le informazioni sul server non sono corrette, ovvero [!DNL Target] non è in grado di accedere al file CSV contenente la definizione dei criteri personalizzati. Modifichiamo i criteri personalizzati per correggerlo.

## Modifica criteri personalizzati

Per modificare i dettagli di una definizione di criteri personalizzata, utilizza la variabile [Modifica API per criteri personalizzati](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom). La sintassi è la seguente:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verifica `TENANT_ID` e `API_KEY`, come prima.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Specifica l’ID dei criteri dei criteri personalizzati (singoli) che desideri modificare.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. Nel corpo, fornisci a JSON aggiornato le informazioni corrette sul server. (Per questo passaggio, specifica l&#39;accesso FTP a un server a cui puoi accedere.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Invia la richiesta e prendi nota della risposta.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Verifica il successo dei criteri personalizzati aggiornati utilizzando **Ottieni API per criteri personalizzati**.

## Ottieni criteri personalizzati

Per visualizzare i dettagli dei criteri personalizzati per uno specifico criterio personalizzato, utilizza la [Ottieni API per criteri personalizzati](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). La sintassi è la seguente:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Specifica l&#39;ID dei criteri personalizzati di cui desideri ottenere i dettagli. Invia la richiesta e controlla la risposta.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Verifica il successo. (Nel nostro caso, verifica che non ci siano ulteriori errori FTP.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Facoltativo) Verifica che l’aggiornamento si rifletta con precisione nell’interfaccia utente.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Elimina criteri personalizzati

Utilizzando l&#39;ID criteri indicato in precedenza, elimina i criteri personalizzati utilizzando [Elimina API per criteri personalizzati](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom). La sintassi è la seguente:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Specifica l’ID dei criteri dei criteri personalizzati (singoli) che desideri eliminare. Fai clic su **Send** (Invia).
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Verifica che i criteri siano stati eliminati utilizzando Ottieni criteri personalizzati.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
In questo caso, l’errore 404 previsto indica che i criteri eliminati non possono essere trovati.

>[!NOTE]
>Come promemoria, i criteri non verranno rimossi dal [!DNL Target] Interfaccia utente anche se è stata eliminata, perché è stata creata utilizzando l’API Crea criterio personalizzato.

Congratulazioni! Ora puoi creare, elencare, modificare, eliminare e ottenere dettagli sui criteri personalizzati, utilizzando [!DNL Recommendations] API. Nella sezione successiva, utilizzerai il [!DNL Target] API di consegna per recuperare i consigli.

[Successivo &quot;Recupera Recommendations con API di distribuzione lato server&quot; >](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=&quot;_blank&quot;}
