---
title: Come configurare l’autenticazione per le API di Adobe Target
description: Questa esercitazione guida gli sviluppatori attraverso i passaggi necessari per generare i token di autenticazione necessari per interagire con successo con le API di Adobe Target. Segui questi passaggi per utilizzare Adobe Developer Console per generare e testare il token di accesso al portatore, necessario per utilizzare le API di Target.
role: Developer, Administrator, Architect
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Administration & Configuration
doc-type: tutorial
kt: null
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: 2c371ea17ce38928bcf3655a0d604a69e29963a0
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 2%

---


# Configurare l’autenticazione per le API di Adobe Target

Le API amministratore di Adobe Target, comprese le [!DNL Recommendations] API amministratore, sono protette dall’autenticazione per garantire che solo gli utenti autorizzati le utilizzino per accedere ad Adobe Target. Utilizza [Adobe Developer Console](https://console.adobe.io/) per gestire questa autenticazione per tutte le soluzioni Adobe Experience Cloud, incluso [!DNL Target].

Questa lezione illustra i passaggi preliminari necessari per generare i token di autenticazione necessari per interagire con successo con le API di Adobe Target. Nelle sezioni seguenti, eseguirai le operazioni riportate di seguito.

1. Crea un progetto (precedentemente denominato integrazione) in Adobe Developer Console.
2. Esporta i dettagli del progetto in Postman.
3. Genera un token di accesso al portatore.
4. Verifica il token di accesso al portatore.

## Prerequisiti

| Risorsa | Dettagli |
| --- | --- |
| Postman | Per completare questi passaggi con successo, ottieni l&#39; [app Postman](https://www.postman.com/downloads/) per il tuo sistema operativo. Postman Basic è gratuito con la creazione dell&#39;account. Anche se non è necessario per utilizzare le API di Adobe Target in generale, Postman semplifica i flussi di lavoro API e Adobe Target fornisce diverse raccolte Postman per aiutarti a eseguire le API e imparare come funzionano. Il resto di questo tutorial presuppone la conoscenza di lavoro di Postman. Per assistenza, fai riferimento alla [documentazione Postman](https://learning.getpostman.com/). |
| Riferimenti | Nel resto dell’esercitazione viene utilizzata la familiarità con le seguenti risorse:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentazione di Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentazione API di Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Creare un progetto di Adobe I/O

In questa sezione potrai accedere ad Adobe Developer Console e creare un progetto per [!DNL Adobe Target]. Per ulteriori informazioni, consulta la documentazione [sui progetti](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md).

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. In [Adobe Admin Console](https://adminconsole.adobe.com/), assicurati che al tuo account utente Adobe sia stato concesso l&#39;accesso a livello di [Amministratore prodotto](https://helpx.adobe.com/enterprise/using/admin-roles.html) e [Sviluppatore](https://helpx.adobe.com/enterprise/using/manage-developers.html) a [!DNL Target].

2. In [Adobe Developer Console](https://console.adobe.io/), seleziona l&#39;organizzazione Experience Cloud per la quale desideri creare questa integrazione. (È probabile che tu possa avere accesso solo a una singola organizzazione Experience Cloud.)

   ![configure-io-target-createproject2.png](assets/configure-io-target-createproject2.png)

3. Fai clic su **[!UICONTROL Crea nuovo progetto]**.

   ![configure-io-target-createproject3.png](assets/configure-io-target-createproject3.png)

4. Fai clic su **[!UICONTROL Aggiungi API]** per aggiungere un’API REST al progetto per accedere ai servizi e ai prodotti di Adobe.

   ![Aggiungi API](assets/configure-io-target-createproject4.png)

5. Seleziona **[!DNL Adobe Target]** come servizio Adobe con cui desideri eseguire l’integrazione. Fare clic sul pulsante **[!UICONTROL Avanti]** visualizzato.

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

6. Seleziona un’opzione per associare le chiavi pubblica e privata all’integrazione dell’account di servizio che stai creando per Target. Per questa esercitazione, seleziona **[!UICONTROL Opzione 1: Genera una coppia di chiavi]** e fai clic su **[!UICONTROL Genera una coppia di chiavi]**.
   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

7. Notate i risultati! Come indicato, prendi nota del file di configurazione scaricato automaticamente (`config`), che contiene la tua chiave privata. Fai clic su **[!UICONTROL Successivo]**.
   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)
8. Nel file system, verifica la posizione di `config`, che è il file di configurazione compresso creato nel passaggio precedente. Anche in questo caso, questo file `config` contiene la tua chiave privata, di cui avrai bisogno in un secondo momento. La posizione esatta all&#39;interno del file system può essere diversa da quella mostrata qui.
   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)
9. Sempre in Adobe Developer Console, seleziona i [profili di prodotto](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) corrispondenti alle proprietà in cui utilizzi [!DNL Recommendations]. Se non utilizzi le proprietà, seleziona l’opzione Area di lavoro predefinita. Fai clic su **[!UICONTROL Salva API configurata]**.
   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

10. Fai clic su **[!UICONTROL Crea integrazione]**. Dovresti ricevere un messaggio temporaneo per indicare che l’API è stata configurata correttamente.

11. Come passaggio finale, rinomina il progetto in un nome più significativo dell’ `Project 1` originale. A questo scopo, accedi al progetto utilizzando il percorso di navigazione mostrato, fai clic su **[!UICONTROL Modifica progetto]** per accedere al modale **[!UICONTROL Modifica progetto] e rinomina il progetto.

![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>In questa esercitazione, chiamiamo il nostro progetto &quot;Integrazione Target&quot;. Se prevedete di utilizzare il progetto per più di Adobe Target, potreste voler denominarlo di conseguenza. Ad esempio, puoi scegliere di denominarlo &quot;API di Adobe&quot; o &quot;API di Experience Cloud&quot;, in quanto può essere utilizzato con altre soluzioni in Adobe Experience Cloud.

## Esportare i dettagli del progetto

Ora che disponi di un progetto di Adobe da utilizzare per accedere a [!DNL Target], assicurati di inviare i dettagli di tale progetto insieme alle richieste API Adobi. Questi dettagli sono necessari per interagire con diverse API di Adobe, tra cui diverse API [!DNL Target]. Ad esempio, i dettagli dell’integrazione includono le informazioni di autorizzazione e autenticazione richieste dalle [!DNL Target] API amministratore. Pertanto, per utilizzare le API con Postman, devi inserire tali dettagli in Postman.

Ci sono molti modi per specificare i dettagli del progetto in Postman, ma in questa sezione utilizziamo alcune funzioni e raccolte predefinite. Innanzitutto (in questa sezione), esporterai i dettagli della tua integrazione in un ambiente Postman. Quindi (nella sezione seguente), genererai un token di accesso al portatore per concederti l’accesso alle risorse di Adobe necessarie.

>[!NOTE]
>
>Per le istruzioni video applicabili a qualsiasi soluzione di Experience Cloud, tra cui [!DNL Target], consulta [Utilizzare Postman con API di Experience Platform](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html). Le sezioni seguenti sono pertinenti alle API [!DNL Target] :
>
> 1. Esportare i dettagli di integrazione di Adobi I/O in Postman
> 2. Generare un token di accesso con Postman

>
> 
Questi passaggi sono forniti anche di seguito.

1. Sempre in [Adobe Developer Console](https://console.adobe.io/), accedi a per visualizzare le credenziali **[!UICONTROL Service Account (JWT)]** del nuovo progetto. Utilizza la navigazione a sinistra o la sezione **[!UICONTROL Credenziali]** come mostrato.
   ![JWT1](assets/configure-io-target-jwt1.png)
Nei dettagli  **[!UICONTROL delle credenziali]**, puoi visualizzare le tue chiavi  **pubbliche,** l&#39;ID  **client** e altre informazioni relative al tuo account del servizio.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. Fai clic su per accedere alle informazioni sull’ API **[!UICONTROL Adobe Target]**. Utilizza la navigazione a sinistra o la sezione **[!UICONTROL Prodotti e servizi collegati]** come mostrato.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Fai clic su **[!UICONTROL Scarica per Postman]** > **[!UICONTROL Account di servizio (JWT)]** per creare un file JSON che acquisisca le informazioni di autenticazione per un ambiente Postman.
   ![JWT3](assets/configure-io-target-jwt3.png)
Prendi nota del file JSON nel tuo file system.
   ![JWT3A](assets/configure-io-target-jwt3a.png)
4. In Postman, fai clic sull&#39;icona a forma di ingranaggio per gestire gli ambienti, quindi fai clic su **Importa** per importare il file JSON (ambiente).
   ![JWT4](assets/configure-io-target-jwt4.png)
5. Scegli il file e fai clic su **Apri**.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. Nel modale Postman **Manage Environments** , fai clic sul nome dell’ambiente appena importato per ispezionarlo. Il nome dell’ambiente può essere diverso da quello mostrato qui. Modificate il nome come desiderato. Non deve necessariamente corrispondere al nome del progetto di Adobe.)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. I valori delle note `CLIENT_SECRET` e `API_KEY` (insieme ad altre variabili) sono precompilati, a partire dall’integrazione definita in Adobe Developer Console. (La variabile Postman `CLIENT_SECRET` deve corrispondere alla credenziale di Adobe `CLIENT SECRET` visualizzata nella Console per sviluppatori e `API_KEY` in Postman deve corrispondere allo stesso modo a `CLIENT ID` nella Console per sviluppatori.) Al contrario, le note `PRIVATE_KEY`, `JWT_TOKEN` e `ACCESS_TOKEN` sono vuote. Cominciamo fornendo il valore `PRIVATE_KEY`.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**Sorpresa!**
   >
   >Quiz pop! Riuscite a ricordarvi dov&#39;è la vostra chiave privata?
   >Esatto, si trova nel file `config` scaricato in precedenza da Adobe Developer Console!

8. Dal file system, apri il file `config` e il file di chiave `private`.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. Seleziona e copia l&#39;intero contenuto del file di chiave `private`.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. In Postman, incolla il valore della chiave privata nei campi **VALORE INIZIALE** e **VALORE CORRENTE** .
   ![JWT10](assets/configure-io-target-jwt10.png)
11. Fai clic su **[!UICONTROL Aggiorna]** e chiudi il modale Ambienti .


## Genera il token di accesso al portatore

In questa sezione viene generato il token di accesso al portatore, necessario per l’autenticazione dell’interazione con le API di Adobe Target. Per generare il token di accesso al portatore, devi inviare i dettagli di integrazione (stabiliti nelle sezioni precedenti) al servizio [Adobe Identity Management Service (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Esistono diversi modi per eseguire questa operazione, ma in questa esercitazione è possibile generare una richiesta POST personalizzata per l’API IMS. Sto scherzando. In questa esercitazione, sfruttiamo una raccolta Postman contenente una chiamata IMS predefinita che rende il processo diretto e semplice. Una volta importata la raccolta, puoi riutilizzarla ogni volta che necessario per generare nuovi token non solo per Adobe Target, ma anche per altre API di Adobe.

1. Passa alle chiamate di esempio [API di Identity Management Service di Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).
   ![token1](assets/configure-io-target-generatetoken1.png)
2. Fai clic sulla raccolta di Postman per la generazione di token di accesso di Adobe I/O **.**
   ![token2](assets/configure-io-target-generatetoken2.png)
3. Ottieni il JSON non elaborato per questa raccolta facendo clic su **Raw**, quindi copia il JSON risultante negli Appunti. In alternativa, puoi salvare il JSON non elaborato come file .json.
   ![token3](assets/configure-io-target-generatetoken3.png)
4. In Postman, importa la raccolta incollando e inviando il JSON non elaborato dagli Appunti. In alternativa, puoi caricare il file .json salvato. Fate clic su **Continue** (Continua).
   ![token4](assets/configure-io-target-generatetoken4.png)
5. Seleziona **[!UICONTROL IMS: JWT Genera + Auth tramite la richiesta User Token]** nella raccolta Adobe I/O Access Token Generation Postman , accertati che l&#39;ambiente sia selezionato e fai clic su **Invia** per generare il token.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Questo token di accesso al portatore sarà valido per 24 ore. Invia nuovamente la richiesta ogni volta che devi generare un nuovo token.

6. Apri nuovamente la finestra modale Gestisci ambienti e seleziona l’ambiente.
   ![token6](assets/configure-io-target-jwt11.png)
7. I valori `ACCESS_TOKEN` e `JWT_TOKEN` sono ora compilati.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>D: Devo utilizzare la raccolta Postman di generazione del token di accesso Adobe I/O per generare il token di accesso JSON Web Token (JWT) e il token di accesso al portatore?
>
>R: No! La raccolta Postman di generazione del token di accesso Adobe I/O è disponibile come comodità per generare più facilmente il token di accesso JWT e al portatore in Postman. In alternativa, puoi utilizzare le funzionalità di Adobe Developer Console per generare manualmente il token di accesso al portatore.

## Test del token di accesso al portatore

In questo esercizio, utilizzerai il nuovo token di accesso al portatore inviando una richiesta API che recupera un elenco di attività dal tuo account [!DNL Target]. Una risposta corretta indica che il progetto di Adobe e l’autenticazione funzionano come previsto per poter utilizzare l’API.

1. Importa la [raccolta Postman API di amministrazione Adobe Target](https://developers.adobetarget.com/api/#admin-postman-collection). Segui tutti i prompt fino a quando la raccolta non viene importata in Postman.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. Espandi la raccolta e prendi nota della richiesta **[!UICONTROL Elenca attività]** .
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. Tieni presente che le variabili come `{{access_token}}` inizialmente non sono risolte. Puoi risolvere il problema in diversi modi, ad esempio, puoi definire una nuova variabile di raccolta denominata `{{access_token}}`, ma in questa esercitazione modificherai la richiesta API per sfruttare l’ambiente Postman che stavi utilizzando in precedenza. In questo modo l’ambiente continuerà a fungere da unico consolidamento coerente di tutte le variabili comuni tra le API di Adobe.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. Digitare per sostituire `{{access_token}}` con `{{ACCESS_TOKEN}}`.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. Digitare per sostituire `{{api_key}}` con `{{API_KEY}}`.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. Digitare per sostituire `{{tenant}}` con `{{TENANT_ID}}`. Nota `{{TENANT_ID}}` non ancora riconosciuta.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. Apri la finestra modale Manage Environments (Gestisci ambienti) e seleziona l’ambiente.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. Digitare per aggiungere una nuova variabile di ambiente `{{TENANT_ID}}`. Copia e incolla il valore dell’ID tenant nei campi **VALORE INIZIALE** e **VALORE CORRENTE** per la nuova variabile di ambiente `TENANT_ID`.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >L&#39;ID tenant è diverso dal [!DNL Target] `clientcode`. L’ID tenant esiste nell’URL quando si effettua l’accesso a [!DNL Target]. Per ottenere il tuo ID tenant, accedi a [!DNL Adobe Experience Cloud], apri [!DNL Target] e fai clic sulla scheda [!DNL Target] . Utilizza il valore ID tenant come indicato nel sottodominio URL.
   >
   >Ad esempio, se l’URL al momento dell’accesso ad Adobe Target è
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >il tuo ID tenant è quindi &quot;la mia azienda&quot;.

1. Invia la richiesta dopo aver verificato la corretta selezione dell’ambiente. Dovresti ricevere una risposta contenente il tuo elenco di attività.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

Congratulazioni! Dopo aver verificato l’autenticazione dell’Adobe, puoi utilizzarla per interagire con le API Adobe Target (e con altre API di Adobe). Ad esempio, puoi [utilizzare le API di Recommendations](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html) per creare o gestire i consigli.
