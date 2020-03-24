---


---

<p>主要是用于在生产环境中为用户在本地创建一个service worker 来缓存资源到本地，提升应用的访问速度</p>
<p>/* eslint-disable no-use-before-define */</p>
<p>// In production, we register a service worker to serve assets from local cache.</p>
<p>// This lets the app load faster on subsequent visits in production, and gives</p>
<p>// it offline capabilities. However, it also means that developers (and users)</p>
<p>// will only see deployed updates on the “N+1” visit to a page, since previously</p>
<p>// cached resources are updated in the background.</p>
<p>// To learn more about the benefits of this model, read <a href="https://goo.gl/KwvDNy">https://goo.gl/KwvDNy</a>.</p>
<p>// This link also includes instructions on opting out of this behavior.</p>
<p>const  isLocalhost = Boolean(</p>
<p>window.location.hostname === ‘localhost’</p>
<p>// [::1] is the IPv6 localhost address.</p>
<p>|| window.location.hostname === ‘[::1]’</p>
<p>// 127.0.0.1/8 is considered localhost for IPv4.</p>
<p>|| window.location.hostname.match(/^127(?:.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)){3}$/),</p>
<p>);</p>
<p>export  default  function  register() {</p>
<p>if (process.env.NODE_ENV === ‘production’ &amp;&amp; ‘serviceWorker’  in  navigator) {</p>
<p>// The URL constructor is available in all browsers that support SW.</p>
<p>const  publicUrl = new  URL(process.env.PUBLIC_URL, window.location);</p>
<p>if (publicUrl.origin !== window.location.origin) {</p>
<p>// Our service worker won’t work if PUBLIC_URL is on a different origin</p>
<p>// from what our page is served on. This might happen if a CDN is used to</p>
<p>// serve assets; see <a href="https://github.com/facebookincubator/create-react-app/issues/2374">https://github.com/facebookincubator/create-react-app/issues/2374</a></p>
<p>return;</p>
<p>}</p>
<p>window.addEventListener(‘load’, () =&gt; {</p>
<p>const  swUrl = ‘service-worker.js’;</p>
<p>if (isLocalhost) {</p>
<p>// This is running on localhost. Lets check if a service worker still exists or not.</p>
<p>checkValidServiceWorker(swUrl);</p>
<p>// Add some additional logging to localhost, pointing developers to the</p>
<p>// service worker/PWA documentation.</p>
<p>navigator.serviceWorker.ready.then(() =&gt; {</p>
<p>console.log(</p>
<p>'This web app is being served cache-first by a service ’</p>
<ul>
<li>‘worker. To learn more, visit <a href="https://goo.gl/SC7cgQ">https://goo.gl/SC7cgQ</a>’,</li>
</ul>
<p>);</p>
<p>});</p>
<p>} else {</p>
<p>// Is not local host. Just register service worker</p>
<p>registerValidSW(swUrl);</p>
<p>}</p>
<p>});</p>
<p>}</p>
<p>}</p>
<p>function  registerValidSW(swUrl) {</p>
<p>navigator.serviceWorker</p>
<p>.register(swUrl)</p>
<p>.then((registration) =&gt; {</p>
<p>registration.onupdatefound = () =&gt; {</p>
<p>const  installingWorker = registration.installing;</p>
<p>installingWorker.onstatechange = () =&gt; {</p>
<p>if (installingWorker.state === ‘installed’) {</p>
<p>if (navigator.serviceWorker.controller) {</p>
<p>// At this point, the old content will have been purged and</p>
<p>// the fresh content will have been added to the cache.</p>
<p>// It’s the perfect time to display a "New content is</p>
<p>// available; please refresh." message in your web app.</p>
<p>console.log(‘New content is available; please refresh.’);</p>
<p>} else {</p>
<p>// At this point, everything has been precached.</p>
<p>// It’s the perfect time to display a</p>
<p>// “Content is cached for offline use.” message.</p>
<p>console.log(‘Content is cached for offline use.’);</p>
<p>}</p>
<p>}</p>
<p>};</p>
<p>};</p>
<p>})</p>
<p>.catch((error) =&gt; {</p>
<p>console.error(‘Error during service worker registration:’, error);</p>
<p>});</p>
<p>}</p>
<p>function  checkValidServiceWorker(swUrl) {</p>
<p>// Check if the service worker can be found. If it can’t reload the page.</p>
<p>fetch(swUrl)</p>
<p>.then((response) =&gt; {</p>
<p>// Ensure service worker exists, and that we really are getting a JS file.</p>
<p>if (</p>
<p>response.status === 404</p>
<p>|| response.headers.get(‘content-type’).indexOf(‘javascript’) === -1</p>
<p>) {</p>
<p>// No service worker found. Probably a different app. Reload the page.</p>
<p>navigator.serviceWorker.ready.then((registration) =&gt; {</p>
<p>registration.unregister().then(() =&gt; {</p>
<p>window.location.reload();</p>
<p>});</p>
<p>});</p>
<p>} else {</p>
<p>// Service worker found. Proceed as normal.</p>
<p>registerValidSW(swUrl);</p>
<p>}</p>
<p>})</p>
<p>.catch(() =&gt; {</p>
<p>console.log(‘No internet connection found. App is running in offline mode.’);</p>
<p>});</p>
<p>}</p>
<p>export  function  unregister() {</p>
<p>if (‘serviceWorker’  in  navigator) {</p>
<p>navigator.serviceWorker.ready.then((registration) =&gt; {</p>
<p>registration.unregister();</p>
<p>});</p>
<p>}</p>
<p>}</p>

