---
title: Come gestire il catalogo Recommendations utilizzando le API
description: Questa parte dell’esercitazione guida gli sviluppatori attraverso i passaggi necessari per utilizzare le API di Adobe Target per creare, aggiornare, salvare, ottenere ed eliminare entità nel catalogo Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 8060b69b-e8e5-4fe7-895f-742410d8ed45
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 2%

---

# Gestire il catalogo [!DNL Recommendations] utilizzando le API

A questo punto, hai imparato a generare un token di accesso, utilizzando il flusso di autenticazione JWT, per utilizzare le API amministratore di Adobe Target con Adobe I/O.

You can use the [Recommendations APIs](https://developers.adobetarget.com/api/recommendations/) to add, update, or delete items in your recommendations catalog. Come per le altre API amministratore di Adobe Target, le API [!DNL Recommendations] richiedono l’autenticazione.

>[!TIP]
>
>Send the **[!UICONTROL IMS: JWT Generate + Auth via User Token]** request whenever you need to refresh your access token for authentication, since it expires after 24 hours. Per istruzioni, consulta [Configurare l&#39;autenticazione API Adobe](../apis/configure-io-target-integration.md) .

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>Prima di procedere, ottieni la [raccolta Recommendations Postman](https://developers.adobetarget.com/api/recommendations/#section/Postman).

## Creazione e aggiornamento di elementi con l’API Save Entities

Per compilare il database di prodotti [!DNL Recommendations] utilizzando l&#39;API anziché un feed di prodotto CSV o le richieste [!DNL Target] che si attivano sulle pagine dei prodotti, utilizza l&#39; [Save Entities API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities). Questa richiesta aggiunge o aggiorna un elemento in un singolo ambiente [!DNL Target]. La sintassi è la seguente:

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

Ad esempio, Save Entities può essere utilizzato per aggiornare gli articoli ogni volta che vengono soddisfatte determinate soglie, come le soglie per l&#39;inventario o il prezzo, al fine di contrassegnare tali articoli e impedirne l&#39;utilizzo consigliato.

1. Passa a **[!DNL Target]> [!UICONTROL Configurazione] > [!UICONTROL Host] > [!UICONTROL Ambienti]** per ottenere l&#39; [!DNL Target] ID ambiente in cui desideri aggiungere o aggiornare un elemento.

   ![SaveEntities1](assets/SaveEntities01.png)

2. Verifica che `TENANT_ID` e `API_KEY` facciano riferimento alle variabili di ambiente Postman stabilite in precedenza. Usa l&#39;immagine seguente per un confronto. Se necessario, modifica le intestazioni e il percorso nella richiesta API in modo che corrispondano a quelli nell’immagine seguente.

   ![SaveEntities3](assets/SaveEntities03.png)

3. Immetti il tuo codice JSON come **raw** nel **Body**. Non dimenticare di specificare l’ID ambiente utilizzando la variabile `environment` . Nell’esempio seguente, l’ID ambiente è 6781.

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   Di seguito è riportato un esempio di JSON che aggiunge entity.id kit2001 con i valori di entità associati per un prodotto Toaster Oven, nell&#39;ambiente 6781.

   ```
      {
      "entities": [{
              "name": "Toaster Oven",
              "id": "kit2001",
              "environment": 6781,
              "categories": [
                  "housewares:appliances"
              ],
              "attributes": {
                  "inventory": 77,
                  "margin": 23,
                  "message": "crashing helicopter",
                  "pageUrl": "www.foobar.foo.com/helicopter.html",
                  "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
              }
          }]
      }
   ```

4. Fai clic su **Send** (Invia). Dovresti ricevere la seguente risposta.

   ![SaveEntities5.png](assets/SaveEntities05.png)

L’oggetto JSON può essere ridimensionato per inviare più prodotti. Ad esempio, questo JSON specifica due entità.

```
    {
        "entities": [{
                "name": "Toaster Oven",
                "id": "kit2001",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 89,
                    "margin": 11,
                    "message": "Toaster Oven",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 102.5
                }
            },
            {
                "name": "Blender",
                "id": "kit2002",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 36,
                    "margin": 5,
                    "message": "Blender",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 54.5
                }
            }
        ]
    }
```

1. Adesso tocca a te! Use the **Save Entities** API to add the following items to your catalog. Utilizza il JSON campione sopra come punto iniziale. Per includere altre entità, è necessario estendere il JSON.

   ![SaveEntities6.png](assets/SaveEntities06.png)

Wow, sembra che gli ultimi due oggetti non appartengano. Esaminiamole utilizzando l&#39;API **Ottieni entità** e, se necessario, eliminale utilizzando l&#39;API **Elimina entità**.

## Ottenimento dei dettagli degli elementi con l’API Get Entity

Per recuperare i dettagli di un elemento esistente, utilizza [Ottieni API entità](https://developers.adobetarget.com/api/recommendations/#operation/getEntity). La sintassi è la seguente:

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

I dettagli di entità possono essere recuperati solo per una singola entità alla volta. Puoi utilizzare Get Entity per confermare che gli aggiornamenti sono stati effettuati nel catalogo come previsto oppure per controllare in altro modo il contenuto del catalogo.

1. Nella richiesta API, specifica l’ID entità utilizzando la variabile `entityId`. L’esempio seguente restituisce i dettagli per l’entità di cui entityId=kit2004.

   ![GetEntity1](assets/GetEntity1.png)

2. Verifica che `TENANT_ID` e `API_KEY` facciano riferimento alle variabili di ambiente Postman stabilite in precedenza. Usa l&#39;immagine seguente per un confronto. Se necessario, modifica le intestazioni e il percorso nella richiesta API in modo che corrispondano a quelli nell’immagine seguente.

   ![GetEntity2](assets/GetEntity2.png)

3. Invia la richiesta.

   ![GetEntity3](assets/GetEntity3.png)
Se ricevi un errore che indica che l&#39;entità non è stata trovata, come mostrato nell&#39;esempio precedente, verifica che la richiesta venga inviata all&#39; [!DNL Target] ambiente corretto.

   >[!NOTE]
   Se non viene specificato esplicitamente alcun ambiente, Get Entity tenta di ottenere l&#39;entità solo dall&#39; [ambiente predefinito](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=en). If you wish to pull from any environment other than your default environment, you must specify the environment ID.

4. Se necessario, aggiungi il parametro `environmentId` e invia nuovamente la richiesta.

   ![GetEntity4](assets/GetEntity4.png)

5. Send another **Get Entity** request, this time to inspect the entity whose entityId=kit2005.

   ![GetEntity5](assets/GetEntity5.png)

Supponiamo che tu decida che queste entità devono essere rimosse dal catalogo. Usiamo l&#39;API **Elimina entità**.

## Eliminazione di elementi con l’API Elimina entità

Per rimuovere elementi dal catalogo, utilizza l&#39; [Elimina entità API](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities). La sintassi è la seguente:

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
Questa API elimina le entità a cui fanno riferimento gli ID specificati.
If no entity IDs are provided, all entities in the given environment are deleted. Se non viene fornito alcun ID ambiente, le entità verranno eliminate da tutti gli ambienti. Usa questo con cautela!

1. Passa a **[!DNL Target]> [!UICONTROL Configurazione] > [!UICONTROL Host] > [!UICONTROL Ambienti]** per ottenere l’ [!DNL Target] ID ambiente da cui desideri eliminare gli elementi.

   ![DeleteEntities1](assets/SaveEntities01.png)

2. Nella richiesta API, specifica gli ID entità delle entità da eliminare utilizzando la sintassi `&ids=[comma-delimited-entity-ids]` (un parametro di query). Quando elimini più di un&#39;entità, separa gli ID utilizzando una virgola.

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. Specifica l’ID ambiente utilizzando la sintassi `&environment=[environmentId]`, altrimenti le entità in tutti gli ambienti verranno eliminate.

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. Verifica che `TENANT_ID` e `API_KEY` facciano riferimento alle variabili di ambiente Postman stabilite in precedenza. Usa l&#39;immagine seguente per un confronto. Se necessario, modifica le intestazioni e il percorso nella richiesta API in modo che corrispondano a quelli nell’immagine seguente.

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. Invia la richiesta.

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. Verifica i risultati utilizzando **Ottieni entità**, che a questo punto dovrebbe indicare che le entità eliminate non possono essere trovate.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

Congratulazioni! Ora puoi utilizzare le API [!DNL Recommendations] per creare, aggiornare, eliminare e ottenere dettagli sulle entità nel catalogo. Nella sezione successiva verrà illustrato come gestire i criteri personalizzati.

[Avanti &quot;Gestisci criteri personalizzati&quot; >](manage-custom-criteria.md)
