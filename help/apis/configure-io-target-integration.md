---
title: Configurare l'autenticazione per  API Adobe Target
keywords: recommendations;adobe recommendations;premium;api;apis
description: ' Adobe Target Recommendations include un set dedicato di API che consentono di gestire il catalogo di prodotti e/o contenuti raccomandabili; gestire gli algoritmi e le campagne di raccomandazione; e distribuite raccomandazioni in oggetti JSON, HTML o XML da visualizzare in Web, dispositivi mobili, e-mail, IOT e altri canali.'
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 624172d4bc4bc2431ad8af0956c93d3bcc0b9870
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 2%

---


# Configurare l&#39;autenticazione per  API Adobe Target

Le  API di amministrazione Adobe Target, incluse le [!DNL Recommendations] API di amministrazione, sono protette dall&#39;autenticazione per garantire che solo gli utenti autorizzati possano accedervi  Adobe Target. Utilizzate la [ Adobe Developer Console](https://console.adobe.io/) per gestire questa autenticazione per tutte le soluzioni Adobe Experience Cloud, incluso [!DNL Target].

Questa lezione illustra i passaggi preliminari necessari per generare i token di autenticazione necessari per interagire con  API Adobe Target. Nelle sezioni che seguono sarà possibile:

1. Create un progetto (precedentemente denominato integrazione) nella  Adobe Developer Console.
2. Esporta i dettagli del progetto in Postman.
3. Generare un token di accesso al portatore.
4. Verificate il token di accesso del portatore.

## Prerequisiti

| Risorsa | Dettagli |
| --- | --- |
| Postman | Per completare correttamente questi passaggi, è necessario ottenere l&#39; [app Postman](https://www.postman.com/downloads/) per il sistema operativo in uso. Postman Basic è gratuito con la creazione di account. Sebbene non sia richiesto per utilizzare  API Adobe Target in generale, Postman semplifica i flussi di lavoro API e  Adobe Target fornisce diverse raccolte Postman per aiutare a eseguire le sue API e imparare come funzionano. Il resto di questa esercitazione presuppone una conoscenza attiva di Postman. Per assistenza, fare riferimento alla [documentazione Postman](https://learning.getpostman.com/). |
| Riferimenti | Nel resto dell&#39;esercitazione viene utilizzata la familiarità con le seguenti risorse:<UL><li>[ Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentazione su Target  Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentazione API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Creare un progetto Adobe I/O 

In questa sezione, accederete alla  Adobe Developer Console e create un progetto per [!DNL Adobe Target]. Per ulteriori informazioni, fare riferimento alla [documentazione relativa ai progetti](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md).

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. In [Adobe Admin Console](https://adminconsole.adobe.com/), verificare che all&#39;account utente  Adobe sia stato concesso l&#39;accesso a livello di [Amministratore prodotto](https://helpx.adobe.com/enterprise/using/admin-roles.html) e [Sviluppatore](https://helpx.adobe.com/enterprise/using/manage-developers.html) a [!DNL Target].

2. In [ Adobe Developer Console](https://console.adobe.io/), selezionare l&#39;organizzazione  Experience Cloud per la quale si desidera creare questa integrazione. È probabile che abbiate accesso a un&#39;unica organizzazione  Experience Cloud.

   ![configure-io-target-create-project2.png](assets/configure-io-target-createproject2.png)

3. Fare clic su **[!UICONTROL Crea nuovo progetto]**.

   ![configure-io-target-create-project3.png](assets/configure-io-target-createproject3.png)

4. Fate clic su **[!UICONTROL Aggiungi API]** per aggiungere un&#39;API REST al progetto per accedere  servizi e prodotti di Adobe.

   ![Aggiungi API](assets/configure-io-target-createproject4.png)

5. Selezionate **[!DNL Adobe Target]** come servizio di Adobe  con cui desiderate effettuare l&#39;integrazione. Fare clic sul pulsante **[!UICONTROL Next]** che viene visualizzato.

   ![configure-io-target-create-project5](assets/configure-io-target-createproject5.png)

6. Selezionate un&#39;opzione per associare le chiavi pubblica e privata all&#39;integrazione dell&#39;account di servizio che state creando per Target. Per questa esercitazione, selezionare **[!UICONTROL Opzione 1: Generare una coppia di chiavi]** e fare clic su **[!UICONTROL Genera coppia di chiavi]**.
   ![configure-io-target-create-project6](assets/configure-io-target-createproject6.png)

7. Prendete nota dei risultati! Come indicato, prendete nota del file di configurazione scaricato automaticamente (`config`), che contiene la vostra chiave privata. Fai clic su **[!UICONTROL Successivo]**.
   ![configure-io-target-create-project7](assets/configure-io-target-createproject7.png)
8. Nel file system, verificare il percorso di `config`, ovvero il file di configurazione compresso creato nel passaggio precedente. Anche in questo caso, il file `config` contiene la chiave privata, che sarà necessaria, in seguito. La posizione esatta all&#39;interno del file system può essere diversa da quella indicata qui.
   ![configure-io-target-create-project8](assets/configure-io-target-createproject8.png)
9. Nella  console Sviluppatori di Adobe, selezionate i [profili di prodotto](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) corrispondenti alle proprietà in cui si utilizza [!DNL Recommendations]. Se non si utilizzano proprietà, selezionare l&#39;opzione Area di lavoro predefinita. Fare clic su **[!UICONTROL Salva API configurata]**.
   ![configure-io-target-create-project9](assets/configure-io-target-createproject9.png)

10. Fare clic su **[!UICONTROL Crea integrazione]**. Dovreste ricevere un messaggio temporaneo che indica che l&#39;API è stata configurata correttamente.

11. Per concludere, rinominate il progetto in un nome più significativo rispetto all&#39;originale `Project 1`. A questo scopo, andate al progetto utilizzando il percorso di navigazione come mostrato, fate clic su **[!UICONTROL Modifica progetto]** per accedere al modale **[!UICONTROL Modifica progetto] e rinominate il progetto.

![configure-io-target-create-project11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>In questa esercitazione, il nostro progetto è denominato &quot;Integrazione Target&quot;. Se prevedete di utilizzare il progetto per più di  Adobe Target, potete assegnare un nome di conseguenza. Ad esempio, potete scegliere di denominarlo &quot; API di Adobe&quot; o &quot; API di Experience Cloud&quot;, in quanto può essere utilizzato con altre soluzioni nell&#39;Adobe Experience Cloud.

## Esportare i dettagli del progetto

Ora che disponete di un progetto di Adobe  che potete utilizzare per accedere a [!DNL Target], dovete essere certi di inviare i dettagli di tale progetto insieme alle vostre richieste API di Adobe . Questi dettagli sono necessari per interagire con diverse API  Adobe, incluse diverse API [!DNL Target]. Ad esempio, i dettagli di integrazione includono le informazioni di autorizzazione e autenticazione richieste dalle [!DNL Target] API Admin. Pertanto, per utilizzare le API con Postman, è necessario inserire tali dettagli in Postman.

Ci sono molti modi per specificare i dettagli del progetto in Postman, ma in questa sezione, utilizziamo alcune funzioni e raccolte pre-costruite. Innanzitutto (in questa sezione), esportate i dettagli della vostra integrazione in un ambiente Postman. Successivamente (nella sezione seguente), verrà generato un token di accesso al portatore per consentirvi di accedere alle risorse  Adobe necessarie.

>[!NOTE]
>
>Per le istruzioni video applicabili a qualsiasi soluzione  Experience Cloud, inclusa [!DNL Target], vedete [Utilizzare Postman con  API Experience Platform](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html). Le sezioni seguenti riguardano le [!DNL Target] API:
>
> 1. Esporta  dettagli integrazione Adobe I/O in Postman
> 2. Generazione di un token di accesso con Postman

>
> 
Di seguito sono riportati anche questi passaggi.

1. Sempre in [ Adobe Developer Console](https://console.adobe.io/), andate a visualizzare le credenziali **[!UICONTROL Service Account (JWT)]** del nuovo progetto. Utilizzate la navigazione a sinistra o la sezione **[!UICONTROL Credenziali]** come mostrato.
   ![JWT1](assets/configure-io-target-jwt1.png)
Nei dettagli **[!UICONTROL delle]** credenziali, puoi visualizzare le tue chiavi  **pubbliche**, l&#39;ID ****client e altre informazioni relative al tuo account di servizio.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. Fare clic per accedere alle informazioni sull&#39;API **[!UICONTROL Adobe Target]**. Utilizzate la navigazione a sinistra o la sezione **[!UICONTROL Prodotti e servizi collegati]** come mostrato.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Fate clic su **[!UICONTROL Scarica per Postman]** > **[!UICONTROL Account di servizio (JWT)]** per creare un file JSON che acquisisca le informazioni di autenticazione per un ambiente Postman.
   ![JWT3](assets/configure-io-target-jwt3.png)
Notare il file JSON nel file system.
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. In Postman, fai clic sull&#39;icona a forma di ingranaggio per gestire i tuoi ambienti, quindi fai clic su **Importa** per importare il file JSON (ambiente).
   ![JWT4](assets/configure-io-target-jwt4.png)
5. Scegliete il file e fate clic su **Apri**.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. Nella modale Postman **Gestisci ambienti** fare clic sul nome dell&#39;ambiente appena importato per ispezionarlo. Il nome dell’ambiente può essere diverso da quello illustrato di seguito. Modificate il nome come desiderate. Non deve necessariamente corrispondere al nome del progetto del Adobe .)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. Nota `CLIENT_SECRET` e `API_KEY` (insieme ad altre variabili) hanno valori precompilati, a partire dall&#39;integrazione come definito nella  Adobe Developer Console. (La variabile Postman `CLIENT_SECRET` deve corrispondere alla credenziale `CLIENT SECRET`  Adobe visualizzata nella console per sviluppatori e `API_KEY` in Postman deve corrispondere a `CLIENT ID` nella console per sviluppatori.) Al contrario, le note `PRIVATE_KEY`, `JWT_TOKEN` e `ACCESS_TOKEN` sono vuote. Cominciamo fornendo il valore `PRIVATE_KEY`.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**Sorpresa!**
   >
   >Quiz pop! Ricordate dov&#39;è la vostra chiave privata?
   >Esatto, si trova nel file `config` scaricato in precedenza dalla  Adobe Developer Console!

8. Dal file system, aprite il file `config` e aprite il file di chiave `private`.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. Selezionare e copiare l&#39;intero contenuto del file di chiave `private`.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. In Postman, incollate il valore della chiave privata nei campi **VALORE INIZIALE** e **VALORE CORRENTE**.
   ![JWT10](assets/configure-io-target-jwt10.png)
11. Fare clic su **[!UICONTROL Aggiorna]** e chiudere la modale Ambienti.


## Generazione del token di accesso del portatore

In questa sezione viene generato il token di accesso del portatore, richiesto per l&#39;autenticazione dell&#39;interazione con  API Adobe Target. Per generare il token di accesso del portatore, è necessario inviare i dettagli di integrazione (stabiliti nelle sezioni precedenti) al [ Adobe  Identity Management Service (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Esistono diversi modi per farlo, ma in questa esercitazione è possibile creare una richiesta POST personalizzata all&#39;API IMS. Sto scherzando. In questa esercitazione, utilizziamo una raccolta Postman contenente una chiamata IMS precostruita che rende il processo diretto e semplice. Una volta importata la raccolta, potete riutilizzarla ogni volta che sia necessario, per generare nuovi token non solo per  Adobe Target, ma anche per altre API  Adobe.

1. Andate al [Adobe  chiamate di esempio  Identity Management Service API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).
   ![token1](assets/configure-io-target-generatetoken1.png)
2. Fare clic sulla raccolta **Adobe I/O Access Token Generation Postman collection**.
   ![token2](assets/configure-io-target-generatetoken2.png)
3. Ottenete il JSON non elaborato per questa raccolta facendo clic su **Raw**, quindi copiando il JSON risultante negli Appunti. In alternativa, puoi salvare il JSON non elaborato come file .json.
   ![token3](assets/configure-io-target-generatetoken3.png)
4. In Postman, importate la raccolta incollando e inviando il JSON non elaborato dagli Appunti. In alternativa, potete caricare il file .json salvato. Fate clic su **Continue** (Continua).
   ![token4](assets/configure-io-target-generatetoken4.png)
5. Selezionare **[!UICONTROL IMS: JWT Genera + Auth tramite token utente]** richiesta nella raccolta Postman di generazione token di Adobe I/O Access , assicurarsi che l&#39;ambiente sia selezionato e fare clic su **Invia** per generare il token.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Il token di accesso al portatore sarà valido per 24 ore. Inviate di nuovo la richiesta ogni volta che è necessario generare un nuovo token.

6. Apri di nuovo il modale Gestisci ambienti e seleziona il tuo ambiente.
   ![token6](assets/configure-io-target-jwt11.png)
7. I valori `ACCESS_TOKEN` e `JWT_TOKEN` sono ora popolati.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>D: Devo utilizzare la raccolta Postman  generazione token di Adobe I/O Access per generare il token Web JSON (JWT) e il token di accesso del portatore?
>
>A: No! La  raccolta Postman generazione token di Adobe I/O Access è disponibile come comodità per generare più facilmente il token di accesso JWT e il token di accesso del portatore in Postman. In alternativa, potete utilizzare le funzionalità presenti in  Adobe Developer Console per generare manualmente il token di accesso del portatore.

## Test del token di accesso del portatore

In questo esercizio, utilizzerete il nuovo token di accesso al portatore inviando una richiesta API che recupera un elenco di attività dal vostro account [!DNL Target]. Una risposta corretta indica che il progetto  Adobe e l&#39;autenticazione funzionano come previsto per poter utilizzare l&#39;API.

1. Importa la [ Adobe Target Admin APIs Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection). Seguite tutti i prompt fino a quando la raccolta non viene importata in Postman.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. Espandete la raccolta e prendete nota della richiesta **[!UICONTROL Attività elenco]**.
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. Notate che le variabili come `{{access_token}}` inizialmente non sono risolte. Potreste risolvere questo problema in diversi modi, ad esempio, potreste definire una nuova variabile di raccolta denominata `{{access_token}}`, ma in questa esercitazione cambierete la richiesta API per sfruttare l&#39;ambiente Postman precedentemente utilizzato. In questo modo l&#39;ambiente continuerà a fungere da unico consolidamento coerente di tutte le variabili comuni nelle API  Adobe.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. Digitare per sostituire `{{access_token}}` con `{{ACCESS_TOKEN}}`.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. Digitare per sostituire `{{api_key}}` con `{{API_KEY}}`.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. Digitare per sostituire `{{tenant}}` con `{{TENANT_ID}}`. Nota `{{TENANT_ID}}` non ancora riconosciuta.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. Aprite la modale Gestisci ambienti e selezionate il vostro ambiente.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. Digitare per aggiungere una nuova variabile di ambiente `{{TENANT_ID}}`. Copiate e incollate il valore ID tenant nei campi **INITIAL VALUE** e **CURRENT VALUE** per la nuova variabile di ambiente `TENANT_ID`.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >L&#39;ID tenant è diverso dal [!DNL Target] `clientcode`. L&#39;ID tenant esiste nell&#39;URL quando si effettua l&#39;accesso a [!DNL Target]. Per ottenere l&#39;ID tenant, accedete alla [!DNL Adobe Experience Cloud], aprite [!DNL Target] e fate clic sulla scheda [!DNL Target]. Utilizzate il valore ID tenant indicato nel sottodominio URL.
   >
   >Ad esempio, se l’URL al momento dell’accesso a  Adobe Target è
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >quindi il tuo ID tenant è &quot;mycompany&quot;.

1. Inviate la richiesta, dopo aver verificato di aver selezionato l&#39;ambiente corretto. Dovreste ricevere una risposta contenente l&#39;elenco delle attività.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

Congratulazioni! Dopo aver verificato l&#39;autenticazione  Adobe, potete utilizzarla per interagire con  API Adobe Target (così come con altre  API Adobe). Ad esempio, potete [utilizzare le API Recommendations](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html) per creare o gestire le raccomandazioni.
