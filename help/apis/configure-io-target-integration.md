---
title: Come configurare l’autenticazione per le API di Adobe Target
description: Questa esercitazione guida gli sviluppatori attraverso i passaggi necessari per generare i token di autenticazione necessari per interagire con successo con le API di Adobe Target. Segui questi passaggi per utilizzare la console Adobe Developer per generare e testare il token di accesso al portatore, necessario per utilizzare le API di Target.
role: Developer, Admin, Architect
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Administration & Configuration
doc-type: tutorial
kt: null
author: Judy Kim
exl-id: 8a1e93e4-67b2-4942-a8da-fc0f2cbb2df2
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 3%

---

# Configurare l’autenticazione per le API di Adobe Target

API amministratore di Adobe Target, tra cui [!DNL Recommendations] Le API amministratore sono protette dall’autenticazione per garantire che solo gli utenti autorizzati le utilizzino per accedere ad Adobe Target. Utilizza la [Console Adobe Developer](https://console.adobe.io/) per gestire questa autenticazione per tutte le soluzioni Adobe Experience Cloud, tra cui [!DNL Target].

Questa lezione illustra i passaggi preliminari necessari per generare i token di autenticazione necessari per interagire con successo con le API di Adobe Target. Nelle sezioni seguenti, eseguirai le operazioni riportate di seguito.

1. Crea un progetto (precedentemente denominato integrazione) nella console Adobe Developer.
2. Esporta i dettagli del progetto in Postman.
3. Genera un token di accesso al portatore.
4. Verifica il token di accesso al portatore.

## Prerequisiti

| Risorsa | Dettagli |
| --- | --- |
| Postman | Per completare correttamente questi passaggi, ottieni il [app Postman](https://www.postman.com/downloads/) per il sistema operativo in uso. Postman basic è gratuita con la creazione dell’account. Sebbene non sia necessario per utilizzare le API di Adobe Target in generale, Postman semplifica i flussi di lavoro API e Adobe Target fornisce diverse raccolte Postman per aiutarti a eseguire le API e imparare come funzionano. Il resto di questa esercitazione presuppone il funzionamento di Postman. Per assistenza, fare riferimento al [Documentazione di Postman](https://learning.getpostman.com/). |
| Riferimenti | Nel resto dell’esercitazione viene utilizzata la familiarità con le seguenti risorse:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentazione di Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentazione API di Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Creare un progetto di Adobe I/O

In questa sezione puoi accedere alla console Adobe Developer e creare un progetto per [!DNL Adobe Target]. Per ulteriori informazioni, fai riferimento alla [documentazione sui progetti](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md).

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. In [Adobe Admin Console](https://adminconsole.adobe.com/), assicurati che al tuo account utente Adobe siano stati assegnati entrambi [Amministratore del prodotto](https://helpx.adobe.com/enterprise/using/admin-roles.html) e [Sviluppatore](https://helpx.adobe.com/enterprise/using/manage-developers.html) accesso a livello [!DNL Target].

2. In [Console Adobe Developer](https://console.adobe.io/), seleziona l’organizzazione Experience Cloud per la quale desideri creare l’integrazione. (È probabile che tu possa avere accesso solo a una singola organizzazione Experience Cloud.)

   ![configure-io-target-createproject2.png](assets/configure-io-target-createproject2.png)

3. Fai clic su **[!UICONTROL Crea nuovo progetto]**.

   ![configure-io-target-createproject3.png](assets/configure-io-target-createproject3.png)

4. Fai clic su **[!UICONTROL Aggiungi API]** per aggiungere un’API REST al progetto per accedere ai servizi e ai prodotti Adobe.

   ![Aggiungi API](assets/configure-io-target-createproject4.png)

5. Seleziona **[!DNL Adobe Target]** come servizio Adobe con cui desideri effettuare l’integrazione. Fai clic sul pulsante **[!UICONTROL Successivo]** viene visualizzato il pulsante .

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

6. Seleziona un’opzione per associare le chiavi pubblica e privata all’integrazione dell’account di servizio che stai creando per Target. Per questa esercitazione, seleziona **[!UICONTROL Opzione 1: Generare una coppia di chiavi]** e fai clic su **[!UICONTROL Genera coppia di chiavi]**.
   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

7. Notate i risultati! Come indicato, prendi nota del file di configurazione scaricato automaticamente (`config`), che contiene la tua chiave privata. Fai clic su **[!UICONTROL Successivo]**.
   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)
8. Nel file system, verifica il percorso `config`, file di configurazione compresso creato nel passaggio precedente. Ancora una volta, questo `config` il file contiene la chiave privata, di cui avrai bisogno in un secondo momento. La posizione esatta all&#39;interno del file system può essere diversa da quella mostrata qui.
   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)
9. Nella console Adobe Developer, seleziona la [profilo/i di prodotto](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) corrispondente alle proprietà in cui si utilizza [!DNL Recommendations]. Se non utilizzi le proprietà, seleziona l’opzione Area di lavoro predefinita. Fai clic su **[!UICONTROL Salva API configurata]**.
   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

10. Fai clic su **[!UICONTROL Creare un’integrazione]**. Dovresti ricevere un messaggio temporaneo per indicare che l’API è stata configurata correttamente.

11. Come passaggio finale, rinomina il progetto in un nome più significativo dell’originale. `Project 1`. A questo scopo, accedi al progetto utilizzando il percorso di navigazione mostrato, quindi fai clic su **[!UICONTROL Modifica progetto]** per accedere al **[!UICONTROL Modifica progetto] e rinomina il progetto.

![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>In questa esercitazione, chiamiamo il nostro progetto &quot;Integrazione Target&quot;. Se prevedete di utilizzare il progetto per più di Adobe Target, potreste voler denominarlo di conseguenza. Ad esempio, puoi scegliere di denominarlo &quot;API di Adobe&quot; o &quot;API di Experience Cloud&quot;, in quanto può essere utilizzato con altre soluzioni in Adobe Experience Cloud.

## Esportare i dettagli del progetto

Ora che disponi di un progetto di Adobe puoi utilizzare per accedere a [!DNL Target], devi assicurarti di inviare i dettagli di quel progetto insieme alle tue richieste API Adobi. Questi dettagli sono necessari per interagire con diverse API di Adobe, tra cui diverse [!DNL Target] API. Ad esempio, i dettagli dell’integrazione includono le informazioni di autorizzazione e autenticazione richieste dal [!DNL Target] API amministratore. Pertanto, per utilizzare le API con Postman, è necessario inserire tali dettagli in Postman.

In Postman sono disponibili diversi modi per specificare i dettagli del progetto, ma in questa sezione utilizziamo alcune funzioni e raccolte predefinite. Innanzitutto (in questa sezione), esporterai i dettagli della tua integrazione in un ambiente Postman. Quindi (nella sezione seguente), genererai un token di accesso al portatore per concederti l’accesso alle risorse di Adobe necessarie.

>[!NOTE]
>
>Per le istruzioni video applicabili a qualsiasi soluzione di Experience Cloud, tra cui [!DNL Target], vedi [Utilizzare Postman con le API di Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=en). Le sezioni seguenti riguardano [!DNL Target] API:
>
> 1. Esportare i dettagli di integrazione di Adobi I/O in Postman
> 2. Generare un token di accesso con Postman

>
> Questi passaggi sono forniti anche di seguito.

1. Ancora nella [Console Adobe Developer](https://console.adobe.io/), accedi a per visualizzare il nuovo **[!UICONTROL Account di servizio (JWT)]** credenziali. Utilizza la navigazione a sinistra o la **[!UICONTROL Credenziali]** come mostrato.
   ![JWT1](assets/configure-io-target-jwt1.png)
In **[!UICONTROL Dettagli delle credenziali]**, puoi visualizzare il tuo **Chiave pubblica**, **ID client**e altre informazioni relative al tuo account di servizio.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. Fai clic per accedere alle informazioni **[!UICONTROL Adobe Target]** API. Utilizza la navigazione a sinistra o la **[!UICONTROL Prodotti e servizi collegati]** come mostrato.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Fai clic su **[!UICONTROL Scarica per Postman]** > **[!UICONTROL Account di servizio (JWT)]** per creare un file JSON che acquisisca le informazioni di autenticazione per un ambiente Postman.
   ![JWT3](assets/configure-io-target-jwt3.png)
Prendi nota del file JSON nel tuo file system.
   ![JWT3A](assets/configure-io-target-jwt3a.png)
4. In Postman, fai clic sull’icona a forma di ingranaggio per gestire gli ambienti, quindi fai clic su **Importa** per importare il file JSON (ambiente).
   ![JWT4](assets/configure-io-target-jwt4.png)
5. Scegli il file e fai clic su **Apri**.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. In Postman **Gestire gli ambienti** fai clic sul nome dell’ambiente appena importato per esaminarlo. Il nome dell’ambiente può essere diverso da quello mostrato qui. Modificate il nome come desiderato. Non deve necessariamente corrispondere al nome del progetto di Adobe.)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. Nota `CLIENT_SECRET` e `API_KEY` (insieme ad altre variabili) i loro valori sono precompilati, a partire dall’integrazione definita nella console Adobe Developer. (Postman `CLIENT_SECRET` La variabile deve corrispondere a `CLIENT SECRET` le credenziali di Adobe visualizzate nella Console per sviluppatori e `API_KEY` in Postman dovrebbe corrispondere allo stesso modo `CLIENT ID` nella Console per sviluppatori.) Contrariamente, nota `PRIVATE_KEY`, `JWT_TOKEN`e `ACCESS_TOKEN` sono vuote. Cominciamo fornendo il `PRIVATE_KEY` valore.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**Sorpresa!**
   >
   >Quiz pop! Riuscite a ricordarvi dov&#39;è la vostra chiave privata?
   >Esatto, è nel `config` file scaricato in precedenza dalla console Adobe Developer.

8. Dal file system, apri le `config` e aprire il `private` file di chiave.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. Seleziona e copia l’intero contenuto del `private` file di chiave.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. In Postman, incolla il valore della chiave privata nell’ **VALORE INIZIALE** e **VALORE CORRENTE** campi.
   ![JWT10](assets/configure-io-target-jwt10.png)
11. Fai clic su **[!UICONTROL Aggiorna]** e chiudi il modale Ambienti .


## Genera il token di accesso al portatore

In questa sezione viene generato il token di accesso al portatore, necessario per l’autenticazione dell’interazione con le API di Adobe Target. Per generare il token di accesso al portatore, devi inviare i dettagli di integrazione (definiti nelle sezioni precedenti) al [Servizio Adobe Identity Management (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Esistono diversi modi per eseguire questa operazione, ma in questa esercitazione è possibile generare una richiesta POST personalizzata per l’API IMS. Sto scherzando. In questa esercitazione, sfruttiamo una raccolta Postman contenente una chiamata IMS predefinita che rende il processo diretto e semplice. Una volta importata la raccolta, puoi riutilizzarla ogni volta che necessario per generare nuovi token non solo per Adobe Target, ma anche per altre API di Adobe.

1. Passa a [Adobe di chiamate di esempio API del servizio Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).
   ![token1](assets/configure-io-target-generatetoken1.png)
2. Fai clic sul pulsante **Raccolta Postman di Adobe I/O Access Token Generation**.
   ![token2](assets/configure-io-target-generatetoken2.png)
3. Ottieni il JSON non elaborato per questa raccolta facendo clic su **Raw**, quindi copia il JSON risultante negli Appunti. In alternativa, puoi salvare il JSON non elaborato come file .json.
   ![token3](assets/configure-io-target-generatetoken3.png)
4. In Postman, importa la raccolta incollando e inviando il JSON non elaborato dagli Appunti. In alternativa, puoi caricare il file .json salvato. Fate clic su **Continue** (Continua).
   ![token4](assets/configure-io-target-generatetoken4.png)
5. Seleziona la **[!UICONTROL IMS: JWT Genera + Auth tramite token utente]** nell&#39;insieme Adobe I/O Access Token Generation Postman , accertati che l&#39;ambiente sia selezionato e fai clic su **Invia** per generare il token.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Questo token di accesso al portatore sarà valido per 24 ore. Invia nuovamente la richiesta ogni volta che devi generare un nuovo token.

6. Apri nuovamente la finestra modale Gestisci ambienti e seleziona l’ambiente.
   ![token6](assets/configure-io-target-jwt11.png)
7. Tieni presente che `ACCESS_TOKEN` e `JWT_TOKEN` ora vengono compilati.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>D: Devo utilizzare la raccolta Postman Adobe I/O Access Token Generation per generare il token web JSON (JWT) e il token di accesso al portatore?
>
>R: No! L’insieme Adobe I/O Access Token Generation Postman è disponibile per comodità per generare più facilmente il token JWT e di accesso al portatore in Postman. In alternativa, puoi utilizzare le funzionalità di Adobe Developer Console per generare manualmente il token di accesso al portatore.

## Test del token di accesso al portatore

In questo esercizio, utilizzerai il nuovo token di accesso al portatore inviando una richiesta API che recupera un elenco di attività dal tuo [!DNL Target] conto. Una risposta corretta indica che il progetto di Adobe e l’autenticazione funzionano come previsto per poter utilizzare l’API.

1. Importa [Raccolta Postman delle API amministratore di Adobe Target](https://developers.adobetarget.com/api/#admin-postman-collection). Segui tutte le istruzioni finché la raccolta non viene importata in Postman.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. Espandi la raccolta e prendi nota della **[!UICONTROL Elencare attività]** richiesta.
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. Tieni presente che le variabili quali `{{access_token}}` sono inizialmente irrisolti. Puoi risolvere il problema in diversi modi, ad esempio puoi definire una nuova variabile di raccolta denominata `{{access_token}}`- ma in questa esercitazione, modificherai la richiesta API per sfruttare l’ambiente Postman che precedentemente utilizzavi. In questo modo l’ambiente continuerà a fungere da unico consolidamento coerente di tutte le variabili comuni tra le API di Adobe.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. Tipo da sostituire `{{access_token}}` con `{{ACCESS_TOKEN}}`.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. Tipo da sostituire `{{api_key}}` con `{{API_KEY}}`.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. Tipo da sostituire `{{tenant}}` con `{{TENANT_ID}}`. Nota `{{TENANT_ID}}` non è ancora stato riconosciuto.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. Apri la finestra modale Manage Environments (Gestisci ambienti) e seleziona l’ambiente.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. Digitare per aggiungere un nuovo `{{TENANT_ID}}` variabile di ambiente. Copia e incolla il valore dell’ID tenant in **VALORE INIZIALE** e **VALORE CORRENTE** campi per il nuovo `TENANT_ID` variabile di ambiente.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >L’ID tenant è diverso dal tuo [!DNL Target] `clientcode`. L’ID tenant esiste nell’URL quando si effettua l’accesso a [!DNL Target]. Per ottenere il tuo ID tenant, accedi al [!DNL Adobe Experience Cloud], apri [!DNL Target], quindi fai clic su [!DNL Target] il Card. Utilizza il valore ID tenant come indicato nel sottodominio URL.
   >
   >Ad esempio, se l’URL al momento dell’accesso ad Adobe Target è
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >il tuo ID tenant è quindi &quot;la mia azienda&quot;.

1. Invia la richiesta dopo aver verificato la corretta selezione dell’ambiente. Dovresti ricevere una risposta contenente il tuo elenco di attività.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

Congratulazioni! Dopo aver verificato l’autenticazione dell’Adobe, puoi utilizzarla per interagire con le API Adobe Target (e con altre API di Adobe). Ad esempio, puoi [Utilizzare le API di Recommendations](https://developer.adobe.com/target/before-administer/recs-api/){target=_blank} per creare o gestire i consigli.
