---
title: Implementare at.js 2.0 in un’applicazione a pagina singola
description: at.js 2.0 di Adobe Target offre set di funzioni avanzati che consentono di eseguire personalizzazioni su tecnologie lato client di nuova generazione. Segui questi passaggi per implementare at.js 2.0 in un’applicazione a pagina singola.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Implementare at.js 2.0 di Adobe Target in un’applicazione a pagina singola

Adobe Target `at.js` 2.0 offre set di funzioni avanzati che consentono all&#39;azienda di eseguire personalizzazioni su tecnologie lato client di nuova generazione. Questa versione si concentra sull&#39;aggiornamento di `at.js` per garantire interazioni in sintonia con le applicazioni a pagina singola.

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Implementare at.js 2.0 in un’applicazione a pagina singola

* Implementa `at.js` 2.0 in &lt;head> dell&#39;applicazione a pagina singola.
* Implementa la funzione `adobe.target.triggerView()` ogni volta che si cambia la visualizzazione nell&#39;applicazione a pagina singola. A tale scopo è possibile utilizzare diverse tecniche, ad esempio l&#39;ascolto delle modifiche hash degli URL, l&#39;ascolto di eventi personalizzati generati dall&#39;applicazione a pagina singola o l&#39;incorporamento del codice `triggerView()` direttamente nell&#39;applicazione. È consigliabile scegliere l&#39;opzione più adatta per l&#39;applicazione a pagina singola specifica.
* Il nome della visualizzazione è il primo parametro della funzione `triggerView()`. Utilizza nomi semplici, chiari e univoci per semplificarne la selezione nel Compositore esperienza visivo di Target.
* Puoi attivare le visualizzazioni in piccole modifiche di visualizzazione, nonché in contesti non basati su applicazioni a pagina singola, ad esempio a metà strada in una pagina a scorrimento infinito.
* È possibile implementare `at.js` 2.0 e `triggerView()` tramite una soluzione di gestione tag, come Adobe Experience Platform Launch.

## Limitazioni di at.js 2.0

Prima di eseguire l&#39;aggiornamento, tenere presenti le seguenti limitazioni di `at.js` 2.0:

* Il monitoraggio tra più domini non è supportato in `at.js` 2.0
* I parametri mboxOverride.browserIp e mboxSession URL non sono supportati in `at.js` 2.0
* Le funzioni legacy mboxCreate, mboxDefine, mboxUpdate sono obsolete in `at.js` 2.0. Verrà visualizzato il contenuto predefinito e non verranno effettuate richieste di rete.

## Codice piè di pagina della libreria utilizzato nel video

Il codice seguente è stato aggiunto alla sezione Piè di pagina libreria della libreria `at.js` durante il video. Si attiva quando l’app viene caricata per la prima volta e quindi su qualsiasi modifica hash nell’app. Utilizza una versione pulita dell’hash come nome della visualizzazione e &quot;home&quot; quando l’hash è vuoto. Tieni presente che per identificare l’applicazione a pagina singola, il codice cerca il testo &quot;react/&quot; nell’URL, che molto probabilmente dovrà essere aggiornato sul sito. Tieni presente che potrebbe essere più appropriato che l&#39;applicazione a pagina singola attivi `triggerView()` al di fuori degli eventi personalizzati o incorporando il codice direttamente nell&#39;app.

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## Risorse aggiuntive

* [Funzionamento di at.js 2.0 (diagrammi dell&#39;architettura)](understanding-how-atjs-20-works.md)
* [Utilizzare il Compositore esperienza visivo di Adobe Target per applicazioni a pagina singola](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
