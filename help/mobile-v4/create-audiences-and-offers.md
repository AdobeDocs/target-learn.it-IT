---
title: Creare tipi di pubblico e offerte in Adobe Target
description: 'In questa lezione, creiamo tipi di pubblico e offerte in Adobe Target per le tre posizioni implementate nelle lezioni precedenti. Verranno utilizzati per visualizzare esperienze personalizzate nella lezione successiva.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 4b153e4f-a979-49a8-8c26-f7ac95162a2f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 1%

---

# Creare tipi di pubblico e offerte in Adobe Target

In questa lezione, entreremo nell’ interfaccia [!DNL Target] e creeremo tipi di pubblico e offerte per le tre posizioni implementate nelle lezioni precedenti.

## Obiettivi di apprendimento

Al termine di questa lezione, potrai:

* Utilizzo del pubblico in Adobe Target
* Creare offerte in Adobe Target

In particolare, in questa lezione verranno creati tipi di pubblico e offerte necessari per eseguire i casi di utilizzo di personalizzazione definiti all’inizio dell’esercitazione. Vogliamo utilizzare le schermate Home e Ricerca per aiutare gli utenti dell&#39;app a prenotare i loro viaggi e vogliamo usare la schermata di ringraziamento per mostrare alcune promozioni rilevanti in base alla destinazione dell&#39;utente. Ecco una tabella che rappresenta ciò che verrà generato in questa lezione per ogni posizione:

| Posizione | Destinatari | Offerta |
| --- | --- | --- |
| wetravel_Eng_home | Nuovi utenti delle app mobili | &quot;Seleziona la tua origine e destinazione per cercare le rotte disponibili per gli autobus&quot; |
| wetravel_Eng_search | Nuovi utenti delle app mobili | &quot;Utilizza i filtri per limitare i risultati della ricerca&quot; |
| wetravel_Eng_home | Restituzione di utenti di app mobili | &quot;Bentornato! Usa il codice promozionale BACK30 durante il pagamento per ottenere uno sconto del 10%.&quot; |
| wetravel_Eng_search | Restituzione di utenti di app mobili | contenuto predefinito |
| wetravel_context_dest | Destinazione: San Diego | &quot;DJ&quot; |
| wetravel_context_dest | Destinazione: Los Angeles | &quot;Universale&quot; |

## Selezionare l&#39;area di lavoro

Se l&#39;azienda utilizza le proprietà e le aree di lavoro per stabilire i limiti per la personalizzazione di app e siti web e hai implementato il parametro at_property nell&#39;ultima lezione, assicurati innanzitutto di essere nell&#39;area di lavoro corretta prima di procedere con questa lezione. Se non usi Proprietà e Aree di lavoro, ignora questo passaggio. Seleziona l’Area di lavoro utilizzata nella lezione precedente per copiare il valore at_property:

![Esempio in Workspace](assets/workspace.jpg)

## Creare tipi di pubblico

Ora creiamo i tipi di pubblico che utilizzeremo per personalizzare l’app.

### Creare un pubblico per i nuovi utenti

Adobe Target Audiences viene utilizzato per identificare gruppi specifici di visitatori. Le offerte possono quindi essere indirizzate a tali gruppi specifici. Per le prime due posizioni, utilizzeremo un pubblico &quot;Nuovi utenti&quot;:

1. Fai clic su **[!UICONTROL Tipi di pubblico]** nella navigazione superiore.
1. Fai clic sul pulsante **[!UICONTROL Crea pubblico]** .
   ![Creare un nuovo pubblico di utenti](assets/audience_new_mobile_app_users_1.jpg)

1. Immetti **[!UICONTROL Nuovi utenti di app mobili]** come nome del pubblico.
1. Seleziona **[!UICONTROL Aggiungi regola]**.
1. Seleziona una regola **[!UICONTROL Personalizzata]**.
   ![Creare un nuovo pubblico di utenti](assets/audience_new_mobile_app_users_2.jpg)

1. Seleziona **[!UICONTROL a.Launches]**.
1. Seleziona **[!UICONTROL è minore di]**.
1. Immettere **5**.
1. Salva il nuovo pubblico.
   ![Creare un nuovo pubblico di utenti](assets/audience_new_mobile_app_users_3.jpg)

### Creare un pubblico per gli utenti di ritorno

Segui gli stessi passaggi elencati sopra per creare un pubblico per gli utenti fidelizzati.

1. Assegna un nome al pubblico _Restituendo utenti di app mobili_.
1. Utilizza **[!UICONTROL a.Launches è maggiore o uguale a 5]** come regola personalizzata.
1. Salva il nuovo pubblico.

   ![Creare un pubblico di utenti di ritorno](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>Tutte le metriche e le dimensioni del ciclo di vita raccolte nell’ [!DNL Target] SDK per dispositivi mobili sono precedute da &quot;a&quot; (ad esempio, a.Launches) e sono disponibili nell’opzione &quot;Personalizza&quot; del menu a discesa e possono essere utilizzate per creare un pubblico.

### Creare un pubblico per gli utenti Prenotare un viaggio a San Diego

Ora creeremo alcuni tipi di pubblico per alcune delle destinazioni offerte dall&#39;app We.Travel. Nell’ultima lezione abbiamo passato la destinazione come parametro di posizione nella richiesta di posizione wetravel_context_dest . Tale parametro è disponibile nell’opzione &quot;Personalizzato&quot; del menu a discesa.

>[!NOTE]
>
>Se un parametro che si prevede di visualizzare nel menu a discesa Personalizzato non viene visualizzato nell&#39;interfaccia [!DNL Target], controlla che sia effettivamente passato nella richiesta. Se hai verificato che sia presente nella richiesta, ma non è stato caricato nell&#39;interfaccia [!DNL Target], puoi semplicemente digitare il nome del parametro e premere Invio per continuare a definire il pubblico.

1. Denomina il pubblico _Destinazione: San Diego_.
1. Utilizza una regola personalizzata con questa definizione: _locationDest contiene San Diego_.
1. Salva il nuovo pubblico.

   ![Creare il pubblico &quot;San Diego&quot;](assets/audience_locationDest_san_diego.jpg)

### Creare un pubblico per gli utenti Prenotare un viaggio per Los Angeles

1. Denomina il pubblico _Destinazione: Los Angeles_
1. Utilizza una regola personalizzata con questa definizione: _locationDest contiene Los Angeles_
1. Salva il nuovo pubblico.

![Crea pubblico &quot;Los Angeles&quot;](assets/audience_locationDest_los_angeles.jpg)

## Creare offerte

Ora creiamo offerte per visualizzare questi messaggi. Come promemoria, le offerte sono snippet di codice/contenuto, che vengono recapitati nella risposta [!DNL Target] . Vengono create più spesso nell’interfaccia utente [!DNL Target], ma possono anche essere create tramite API o utilizzando l’integrazione Frammenti esperienza con Adobe Experience Manager. Nelle app per dispositivi mobili, le offerte JSON sono comuni. In questa esercitazione utilizzeremo le offerte HTML , che possono essere utilizzate per distribuire qualsiasi contenuto in testo normale (incluso JSON) nell’app.

### Creare l’offerta per i nuovi utenti

Innanzitutto, creiamo offerte per i messaggi ai nuovi utenti:

1. Fai clic su **[!UICONTROL Offerte]** nella navigazione superiore.
1. Fai clic su **[!UICONTROL Crea]**.
1. Seleziona **[!UICONTROL Offerta HTML]**.

   ![Crea offerta principale](assets/offer_home_1.jpg)

1. Denomina l&#39;offerta _Home: Coinvolgi nuovi utenti_.
1. Immetti _Seleziona origine e destinazione per cercare i bus disponibili_ come codice.
1. Salva la nuova offerta.

   ![Crea offerta HTML principale](assets/offer_home_2.jpg)

### Creare l’offerta per gli utenti di ritorno

Ora creiamo l’unica offerta per gli utenti fidelizzati (la seconda offerta sarà il contenuto predefinito, che non verrà visualizzato come nulla):

1. Denomina l&#39;offerta _Home: Restituire utenti_.
1. Inserisci _Bentornato! Usa il codice promozionale BACK30 durante il pagamento per ottenere uno sconto del 10%._ come codice HTML.
1. Salva la nuova offerta.

   ![Crea offerta HTML principale](assets/offer_home_returning_users.jpg)

### Creare l’offerta San Diego

Quando si restituisce &quot;DJ&quot; all&#39;attività di ringraziamento, nella logica della funzione filterRecommendationBasedOnOffer() viene visualizzato un banner per &quot;Rock Night with DJ SAM&quot;:

1. Denomina l&#39;offerta _Promozione per San Diego_.
1. Immetti _DJ_ come codice HTML.
1. Salva la nuova offerta.

![Crea offerta &quot;San Diego&quot;](assets/offer_san_diego.jpg)

### Crea offerta per gli utenti che vanno a Los Angeles

Quando viene restituito &quot;Universal&quot; all&#39;attività di GrazieYou, nella funzione filterRecommendationBasedOnOffer() viene visualizzato un banner per &quot;Universal Studios&quot;:

1. Denomina l&#39;offerta _Promozione per Los Angeles_.
1. Immetti _Universal_ come codice HTML.
1. Salva la nuova offerta.

![Crea offerta &quot;Los Angeles&quot;](assets/offer_los_angeles.jpg)

## Conclusione

Ora abbiamo il nostro pubblico e le nostre offerte. Nella lezione successiva, creeremo attività che legano le posizioni, i tipi di pubblico e le offerte insieme per creare le esperienze personalizzate.

**[SUCCESSIVO : &quot;Personalizza layout&quot; >](personalize-layouts.md)**
