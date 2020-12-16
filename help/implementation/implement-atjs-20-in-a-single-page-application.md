---
title: Implementazione  Adobe Target a.js 2.0 in un'applicazione a pagina singola (SPA)
seo-title: Implementazione  Adobe Target a.js 2.0 in un'applicazione a pagina singola (SPA)
description: La versione più recente di at.js offre set di funzioni avanzati che consentono all’azienda di eseguire personalizzazioni su tecnologie lato client di nuova generazione. Questa nuova versione si concentra sull'aggiornamento di at.js per garantire interazioni in sintonia con le applicazioni a pagina singola.
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 13%

---


# Implementazione  Adobe Target a.js 2.0 in un&#39;applicazione a pagina singola (SPA)

La versione più recente di `at.js` offre set di funzioni avanzate che consentono di eseguire personalizzazioni su tecnologie lato client di nuova generazione. Questa nuova versione è incentrata sull&#39;aggiornamento `at.js` per ottenere interazioni armoniose con applicazioni a pagina singola (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Come implementare a.js 2.0 in un SPA

* Implementare `at.js` 2.0 nella &lt;head> dell&#39;applicazione a pagina singola.
* Implementate la funzione `adobe.target.triggerView()` ogni volta che la visualizzazione cambia nella SPA. A questo scopo possono essere utilizzate diverse tecniche, ad esempio ascolto delle modifiche hash degli URL, ascolto degli eventi personalizzati attivati dal SPA o incorporazione del codice `triggerView()` direttamente nell&#39;applicazione. È consigliabile scegliere l&#39;opzione che funziona meglio per la specifica applicazione a pagina singola.
* Il nome della vista è il primo parametro della funzione `triggerView()`. Utilizzate nomi semplici, chiari e univoci per semplificarne la selezione in Experience Composer (Compositore esperienza visivo) di Target.
* Potete attivare le viste in piccole modifiche di vista, nonché in contesti non SPA come ad esempio a metà strada verso il basso e all’infinito pagina di scorrimento.
* `at.js` 2.0 e  `triggerView()` può essere implementato tramite una soluzione di gestione tag, come  Adobe Experience Platform Launch.

## at.js 2.0 Limitazioni

Prima di eseguire l&#39;aggiornamento, tenere presente i seguenti limiti di `at.js` 2.0:

* Il monitoraggio tra domini diversi non è supportato in `at.js` 2.0
* I parametri URL mboxOverride.browserIp e mboxSession non sono supportati in `at.js` 2.0
* Le funzioni legacy mboxCreate, mboxDefine, mboxUpdate sono obsolete in `at.js` 2.0. Viene visualizzato il contenuto predefinito e non vengono effettuate richieste di rete.

## Codice piè di pagina della libreria utilizzato nel video

Il codice seguente è stato aggiunto alla sezione del piè di pagina della libreria `at.js` durante il video. Viene attivato quando l&#39;app viene caricata per la prima volta e quindi in caso di modifiche hash nell&#39;app. Utilizza una versione ripulita dell&#39;hash come nome della visualizzazione e &quot;home&quot; quando l&#39;hash è vuoto. Per identificare il SPA, il codice cerca il testo &quot;reagisce/&quot; nell&#39;URL, che molto probabilmente dovrà essere aggiornato sul sito. Ricorda anche che potrebbe essere più appropriato che il tuo SPA attivi `triggerView()` eventi personalizzati o incorporando il codice direttamente nella tua app.

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

* [Come funziona at.js 2.0 (diagrammi di architettura)](understanding-how-atjs-20-works.md)
* [Usare  Adobe Target Visual Experience Composer (Compositore esperienza visivo per applicazioni a pagina singola) (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Aggiornamento da at.js 1.x alla documentazione di at.js 2.0](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)