# spiderable WIP
Meteor v1.6+  
Uses google's [puppeteer](https://pptr.dev/)
  
It works great, but code is messy :P

## Install
Add the meteor package
```js
meteor add nooitaf:spiderable
```

## Evironment vars
You can optionaly use the URL to point to a different port, ip or domain.  
Default URL is `http://localhost:3000/`.  

```bash
# examples
export SPIDERABLE_URL="http://localhost:3000/" # default
export SPIDERABLE_TIMEOUT=2000                 # default
export SPIDERABLE_HEADLESS=0                   # 1=enable; 0=disable (default)
export SPIDERABLE_ARGS="['--disable-dev-shm-usage','--no-sandbox']"  # docker
```

## About
`spiderable` is part of [Webapp](https://github.com/meteor/meteor/tree/master/packages/webapp). It's one possible way to allow web search engines to index a Meteor application. It uses the [AJAX Crawling specification](https://developers.google.com/webmasters/ajax-crawling/) published by Google to serve HTML to compatible spiders (Google, Bing, Yandex, and more).

When a spider requests an HTML snapshot of a page the Meteor server runs the client half of the application inside [puppeteer](https://pptr.dev/), a headless chromium browser, and returns the full HTML generated by the client code.

In order to have links between multiple pages on a site visible to spiders, apps must use real links (eg `<a href="/about">`) rather than simply re-rendering portions of the page when an element is clicked. Apps should render their content based on the URL of the page and can use [HTML5 pushState](https://developer.mozilla.org/en-US/docs/DOM/Manipulating_the_browser_history) to alter the URL on the client without triggering a page reload. See the [Todos example](http://meteor.com/examples/todos) for a demonstration.

When running your page, `spiderable` will wait for all publications to be ready. Make sure that all of your [`publish functions`](#meteor_publish) either return a cursor (or an array of cursors), or eventually call [`this.ready()`](#publish_ready). Otherwise, the `puppeteer` executions will timeout.

## Howto see if it's working
Open your page with `http://localhost:3000/?_escaped_fragment_=` should return full html.