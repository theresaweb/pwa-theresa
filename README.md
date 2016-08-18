# pwa-theresa
* A test progressive web app deployed on firebase here, https://pwa-test-3ab3b.firebaseapp.com/work/index.html
* follows https://codelabs.developers.google.com/codelabs/your-first-pwapp
* For local development uses web server for chrome and Chrome dev tools - applications tab https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb?hl=en
* App Shell is cached - these are the core files that provide basic UI and functionality and uses local storage instead of db for ease, not reccomended for prod
* https is required http://www.chromium.org/Home/chromium-security/prefer-secure-origins-for-powerful-new-features
* NOTES FROM CONFERENCE:
native vs web
user has to manage native apps
web safer
web has more reach
users are not adding new apps to their phone
point: web apps provide quality of user experience

User experience needs to be:

* reliable
we assume we're always online

* Performant
20% users drop off after 3 seconds
40% users abandon sites that take longer than 3 seconds to load

* Engaging
web push notifications, 
easy to add to home screen
full screen themeing (immersive)

examples:
* wapo.com/pwa  washtington post, aliexpress (82% inc in conversion on ios)
* smooth scrolling, responsive
* prompts to add to homescreen
* after on homescreen fires up service worker
* runs full screen, no address bar
* works offline

Service workers:
* client side proxy written in js
* second time page is visited, service worker decides how resources are accessed
* can handle push messages


2. https required
3. ground up or single features
  * ground up (e.g. konga.com), start simplified (e.g. washington post (top stories) airberlin focused on post booking experience)
  * or
  * focus on single feature at a time (e.g. weather comapany, focused on push notifications and
     launched push notifications globally  also booking.com and also jumia who added push notifications e.g. when
     shopping cart was abandoned, got 38% open rate of push notifications (9x better rate than email))

* Debugging info https://docs.google.com/document/d/160EgIx-G68pfcKu-jeafAmXViInJin55Dx8IWPTXXXw/view#
* install flow:
  * register service from web page
  * if reg successfull it installs and then in the install phase can prefetch resources, add them to cache
  * add event listener 
  * return control to main page
  * can then alert user it will work offline
    
* service worker is a script that runs in the bg, woken up quickly, service request and then go back to sleep
app doesn't have to be inthe active tab for service worker to run

2 methodologies
* network first (freshest data unless network fails)
* cache first (priority of stale data)

manifest.json
* manifest.json - gives ability to control how app appears where they expect to see it (home screen, task screen)
  * supported by chrome on android not on safari
  * short_name - name on homescreen
  * icons
  * splash screen uses background_color, short name and icon
  * start_url - always starts on this url

* prompt user to install on homescreen when web page is accessed on mobile device
  * prompts if it has following strict requirements
    1. service workers (so works offline) 
    2. manifest.json
    3. user engaged, at least twice in 5 minutes

* Web Push Notifications
  * new to web
  * chrome, FF, opera, coming to Edge, samsung
  * when to use
   * is it important enough
     1. should be timely e.g incoming chat message, calendar events
     2. should be precise, info is good to know and actionable
     3. should be personal

* how push notifications work
* built on service workers
* OS receives notification from endpoint
* 
* subscribing a user
  * check if subscribed
  * ask to subscribe
  * user subscribes
  * subscription object saved on the server

* to send msg
  * message generated on server
  * msg sent to endpoint (central repo, e.g chrome for android GCM)
  * endpoint sends it to browser
  * browser spins up service worker
  * browser handles service worker event
  * browser shows notification

* Voluntary Applicaton Service Identification (VAPID) github.com/web-push-libs/web-push (push library) to get public and private key


* Lighthouse
* Use Lighthouse to establish a baseline
  * lighthouse automates audits for pregressibe web apps github.com/googlechrome/lighthouse
  * can use chrome web tools or command line
  * step through improvements
    * server side rendering, improves time to first paint. content no longer depends on javascript
    * treat service workers as progressive enhancement (example uses app shell(cached aggressively) + dynamic content (loaded after app shell) model)
    
* youtube.com/chromedevelopers
* https://medium.com/@addyosmani/offline-storage-for-progressive-web-apps-70d52695513c#.48604dzel
