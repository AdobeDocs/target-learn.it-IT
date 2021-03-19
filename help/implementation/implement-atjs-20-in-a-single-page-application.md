---
title: Come implementare at.js 2.0 in un’applicazione a pagina singola (SPA)
description: Adobe Target at.js 2.0 offre set di funzioni avanzate che consentono di eseguire personalizzazioni su tecnologie lato client di nuova generazione. Segui questi passaggi per implementare at.js 2.0 in un’applicazione a pagina singola (SPA).
role: Sviluppatori
level: Intermedio
topic: SPA, Architettura, Sviluppo
feature: Implementazione
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Implementare Adobe Target at.js 2.0 in un’applicazione a pagina singola (SPA)

Adobe Target `at.js` 2.0 offre set di funzioni avanzate che consentono di eseguire personalizzazioni su tecnologie lato client di nuova generazione. Questa versione si concentra sull&#39;aggiornamento di `at.js` per garantire interazioni in sintonia con le applicazioni a pagina singola (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Come implementare at.js 2.0 in una SPA

* Implementa `at.js` 2.0 nel &lt;head> dell’applicazione a pagina singola.
* Implementa la funzione `adobe.target.triggerView()` ogni volta che visualizzi le modifiche nel tuo SPA. A questo scopo possono essere utilizzate diverse tecniche, ad esempio l’ascolto delle modifiche dell’hash URL, l’ascolto degli eventi personalizzati attivati dal SPA o l’incorporazione del codice `triggerView()` direttamente nell’applicazione. Scegli l’opzione che funziona meglio per l’applicazione a pagina singola specifica.
* Il nome della visualizzazione è il primo parametro della funzione `triggerView()`. Utilizza nomi semplici, chiari e univoci per facilitarne la selezione nel compositore esperienza visivo di Target.
* È possibile attivare le viste in piccole modifiche di visualizzazione, nonché in contesti non SPA quali la modalità di scorrimento a metà strada di una pagina infinita.
* `at.js` 2.0 e  `triggerView()` può essere implementato tramite una soluzione di gestione tag, come Adobe Experience Platform Launch.

## Limitazioni di at.js 2.0

Prima dell’aggiornamento, tieni presente le seguenti limitazioni di `at.js` 2.0:

* Il monitoraggio tra più domini non è supportato in `at.js` 2.0
* I parametri URL mboxOverride.browserIp e mboxSession non sono supportati in `at.js` 2.0
* Le funzioni legacy mboxCreate, mboxDefine, mboxUpdate sono obsolete in `at.js` 2.0. Verrà visualizzato il contenuto predefinito e non verranno effettuate richieste di rete.

## Codice piè di pagina libreria utilizzato nel video

Il codice seguente è stato aggiunto alla sezione Library Footer della libreria `at.js` durante il video. Viene attivato quando l’app viene caricata per la prima volta e in seguito a eventuali modifiche hash nell’app. Utilizza una versione pulita dell’hash come nome della visualizzazione e &quot;home&quot; quando l’hash è vuoto. Tieni presente che per identificare il SPA, il codice cerca il testo &quot;react/&quot; nell’URL, che molto probabilmente dovrà essere aggiornato sul tuo sito. Tieni presente che potrebbe essere più appropriato che il tuo SPA attivi `triggerView()` eventi personalizzati o incorporando il codice direttamente nell’app.

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

* [Funzionamento di at.js 2.0 (diagrammi di architettura)](understanding-how-atjs-20-works.md)
* [Utilizzare il Compositore esperienza visivo di Adobe Target per le applicazioni a pagina singola (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Aggiornamento da at.js 1.x alla documentazione di at.js 2.0](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)