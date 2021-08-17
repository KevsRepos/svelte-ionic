# Ionic Svelte UI demo
A showcase app for all Ionic UI elements - up to Ionic 5!!! Use this app to try-out the elements you like for your app, and then navigate directly to the API docs or the source code.

Secondly, it is a boilerplate to start developing an Ionic/Svelte/PWA supercharged app (WIP) 

Published as web app: https://ionicsvelte.firebaseapp.com

Hint: try reactivity of the app by using various devices or the Chrome developer view: iOS, Android's material design and fullscreen desktop responsiveness guaranteed!

If you want to run it locally:

```bash
npm install -g degit
degit Tommertom/svelte-ionic-app svelte-ionic-app
cd svelte-ionic-app
npm i
npm run dev
```

Why npm run build sometimes while developing? -> there is a copy script copying many assets to build folder. Having this script run in dev-mode slows down development flow. So strictly spoken, you only need to run this once for this project. So, if you run npm run dev, your assets will be copied. If you want this standard behavior, change rollup.config.js.

The app will be served on `localhost:5000`.

Please note: livereload not enabled (see `rollup.config.js`) because of issue in development environment.

All items also available as individual REPLs: https://github.com/Tommertom/svelte-ionic-app/blob/master/REPLS.md

# User requests
If you have user requests, please raise an issue @ github, or drop a note using the "RateMe" feature in the menu. Some of these comments received and resolved:
- Margin in the SourceViewer
- Stop the begging for Rating

Please check the issue list for other issues resolved. 

I am very happy to get feedback and to make it more usefull to all!

**NEW FEATURE: click to view source! For all components (except tab) you can click the lower right source button to view the source and copy/paste in your app. If you use fullscreen view, the menu will be a sidepanel instead of a hamburger!**

**NEW FEATURE: click on share button in source view to link directly to the Ionic API docs**

**NEW FEATURE: almost all UI elements have a separate REPL (coding playground)**

**NEW FEATURE: Web Animations API included (see Avatars)**

**NEW FEATURE: TYPESCRIPT ARRIVED!!!!! Configuration done and usable via `<script lang="ts">`**

(I just need to add some types to the IonicController.ts so you don't get red curls)

**NEW FEATURE: JAVASCRIPT CODE ADDED!!!**

**NEW FEATURE: RATE ME FEATURE ADDED**

Yes, I like to get your feedback!
And I do wonder why I cant get the navigated URL as a store, so I had to make a separate one...

All features (vision/realised) 
- Rate me - popup to see hear what your user thinks (100%)
- Configured for Typescript usage (100%)
- Web Animations API (see Avatars - 100% done)
- All Ionic Framework UI components showcased (100% done)
- Run as SPA - Filesystem router via Routify (100% done)
- Code splitting - lazy loading of routes (100%)
- Service Worker setup via workbox (75% - not really doing much this way) 
- PWA compliance via Ligthouse score (80% - biggest issue: no 200 when offline)
- RXJS usage (100%)
- Localstorage via localforage (100%)
- Firebase SDK - analytics/firestore (100%)
- Capacitor for mobile native support (100%)
- Ionic Theming in local styles and global CSS (100%)
- REPLs for each element (100%)
- Source code previewer (100%)
- Cookie Popup (100%)
- Ionic included as asset, not CDN (100%)
- Setting global CSS variables - (https://ionicframework.com/docs/theming/css-variables (100%) - see App.svelte)

<img alt="Screen1.PNG" src="https://raw.githubusercontent.com/Tommertom/svelte-ionic-app/master/doc/Screen1.PNG" width="75%" >

And the source view with copy feature and you can select text with the mouse:
<img alt="Screen2.PNG" src="https://raw.githubusercontent.com/Tommertom/svelte-ionic-app/master/doc/Screen2.PNG" width="75%" >

Do you like this work? Please star this project! 

# Known issues

## Not an issue but good to note: Typescript full usage may require typings for some packages
These are not always available for all packages used in this project, and hence not applied.

## Searchbar cancel ionCancel does not fire
I think I need to debug a bit more, because ionInput does fire..... And the show-cancel-button "never" also does not work.

## REPLs are Ionic 4
The REPLs are Ionic 4. I think they still sufficiently serve purpose to play around with the UI, so for now I won't bother too much updating them.

## ion-back-button does not show
Ion Back Button does not appear in the app. Neither in a REPL. Made a custom version.

## Altdetails is not taking the route argument
Needing some debugging - A NAV in the TAB is not working properly

## Capacitor Clipboard on iOS does not copy
Copy of sourcecode on iOS does not seem to work.

## Pane integration is WIP
Pane needs ion-content  to be set to `scroll-y:false` to avoid strange UI on some devices.

## PWA no 200 when offline
This is something that requires a bit more work on my end - finding the right toolbox to do 200 when offline and at the same time a developer friendly implementation for changes. Probably it exists already, but just need to research a bit more.

## Navigation through href isn't as pretty 
In Cards there is a link that navigates away from the current page. It does not nicely replace the page, as it fully reloads. That is not very nice if you ask me, so you have to use a `navigate` method instead of href. That is a bit unfortunate if you ask me (from SEO perspective - correct?)

# Remarks while working on Ionic - Svelte integration

## Setting properties for Ionic Elements
If you want to set properties for Ionic elements, you need to use the `attribute` as defined in the docs. Example:
- not ok: `<ion-content scrollX="true">...</ion-content>`
- ok: `<ion-content scroll-x="true">...</ion-content>`

## Nav needs customElement
Not necessarily an issue, but still a bit undesireable to make a custom element to be using a IonNav (as in `<ion-nav root="my-element">`). Therefore made IonNav.svelte to handle this and developers can include svelte component instead of manually registering a customElement.

## IonTabs selected Tab 
I raised an issue @ Ionic for selected-tab not selecting te default tab as per Ionic's documentation. https://github.com/ionic-team/ionic/issues/20060

## IonNav does not work in tabs
This seems to be related to the ionic router that is not working for me.  IonPage.svelte could be a replacement for a flyin type of animation.

## Want local install of Ionic lib?
Local install (in index.html):
```
    <script type="module" src='/assets/libs/@ionic/core/dist/ionic/ionic.js'></script>
    <link rel="stylesheet" href="/assets/libs/@ionic/core/css/ionic.bundle.css" />
```
Obviously you need to put the NPM lib of @ionic in the assets folder.

# Todo's
A number of todo's:
- Ionic 6 - expected in March?
- Snowpack instead of rollup
- Add some other Ionic things like Platform
- ~~Copy snippets of source code~~
- ~~Implement workbox and spassr as shown in the startertemplate of routify (or at least check) - using https://github.com/OliwerDrywa/svelte-pwa/blob/master/public/service-worker.js~~
- ~~fix IonTab~~
- ~~fix Ionic Menu close, go through all components and fix some messages~~
- ~~research some of the warnings after Ionic 5 migration~~
- ~~Ionic 5 add-ons not present in Ionic 4 (to figure out which ones)~~
- ~~UI elements missing: VirtualScroll skipped~~
- ~~add the popoover and other controller related items~~
- ~~try the css styling as per documentation (theming)~~
- ~~look at awesome rollup and add typescript -~~ not mature enough!!
- ~~fix rollup copy of files in assets folder~~
- ~~do some binding on inputs and other interactive elements~~
- ~~ionicons for menu - colors and other names~~
- ~~ionicons part has some unknown icons, make larger~~
- make it a better PWA - need to work on the service worker - https://developers.google.com/web/tools/workbox/guides/get-started
- ~~better names for controller API?~~
- ~~NAV over tab~~
- ~~make it more sveltish (code, store, bindings, animations)~~
- ~~publish on firebase hosting~~
- ~~try some cordova/ionic native - no web features I need~~
- ~~singleton classes https://alligator.io/js/js-singletons/~~
- ~~place routes in better place (pages folder probably, to avoid repeating /../)~~
- ~~consider Contexts for exposing controllers~~
- ~~split pane~~
- ~~searchbox in ionicons~~
- add non Ionic elements to complete UI: 
    - chat ui and other social elements (https://github.com/thenaim/ionic-tk-social-network)
    - ~~Stimeline~~S
    - accordion
    - ~~pane~~ 
- ~~SSR~~
- ~~to docs link https://ionicframework.com/docs/api/input~~
- https://css-tricks.com/what-i-like-about-writing-styles-with-svelte/
- https://github.com/pngwn/prism-svelte or something else that works
- ~~REPLs~~
- ~~change router? https://github.com/qutran/swheel, https://github.com/jorgegorka/svelte-router/blob/master/README.md~~
- source code formatter in HTML
- Font Awesome icons
- ~~Web Animations API trial - see Avatars~~
- ~~replace manual route filter with ignore option~~
- ~~Sseek ways to include in rollup bundler instead of script include~~S
- ~~SIonic 5 migration - once it is fully released - already some breaking changes~~S

