<ion-menu
  side="{side}"
  content-id="main"
  menu-id="mainmenu"
  class:menuhide="{hideMenu}"
>
  {#if menuItems.length > 0}
    <ion-header>
      <ion-toolbar translucent="true">
        <ion-title>Menu</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-list>
        {#each menuItems as menuItem, i}
          <ion-item
            on:click="{() => {
              closeAndNavigate(menuItem.url);
            }}"
          >
            <ion-icon
              name="{menuItem.icon}"
              slot="start"
              color="{getRandomColor()}"
            ></ion-icon>
            <ion-label>{menuItem.label}</ion-label>
          </ion-item>
        {/each}
        <ion-item></ion-item>
        <ion-item on:click="{goToReview}">
          <ion-icon name="star" slot="start"></ion-icon>
          <ion-label>Rate this app</ion-label>
        </ion-item>
        <ion-item
          on:click="{() => {
            GITHUBclick();
            window.open('https://github.com/Tommertom/svelte-ionic-app', '_blank');
          }}"
        >
          <ion-icon name="logo-github" slot="start"></ion-icon>
          <ion-label>Go to GitHub for this app</ion-label>
        </ion-item>
        <ion-item
          on:click="{() => {
            FORUMclick();
            window.open('https://forum.ionicframework.com/t/ionicsvelte-all-of-ionics-ui-in-one-svelte-app', '_blank');
          }}"
        >
          <ion-icon name="logo-ionic" slot="start"></ion-icon>
          <ion-label>Go to Ionic Forum</ion-label>
        </ion-item>
      </ion-list>
    </ion-content>
  {/if}
</ion-menu>

<style>
ion-item {
  cursor: pointer;
}

.menuhide {
  display: none;
}
</style>

<script lang="ts">
import { fromFetch } from "rxjs/fetch";
import { goto } from "@roxi/routify";
import { getIonicMenu } from "./../services/IonicControllers";

import { routes } from "./../routes/routes";

import { path } from "../services/routestore";

import firebase from "firebase/app";

let hideMenu = true; // a hack because the menu shows before the splash (in Chrome on Windows)
const defaultAnalytics = firebase.analytics();

export let side = "start";

const getRandomColor = () => {
  const items = [
    "secondary",
    "primary",
    "danger",
    "warning",
    "dark",
    "medium",
    "success",
    "tertiary",
  ];
  return items[Math.floor(Math.random() * items.length)];
};

const excludedPaths = [
  "Pane", // buggy component
  "AltDetails",
  "ModalExtra",
  "NavDetail",
  "NavList",
  "Games",
  "Music",
  "PopoverExtra",
];

// let's use the generated routes for making the menu items
// and skip a few ones for the menu
let menuItems: Array<{ url: string; label: string; icon: string }> = routes
  .filter((route) => route.path.includes("ionic"))
  .filter((route) => {
    let found = false;
    excludedPaths.forEach((exclude) => {
      found = found || route.path.includes(exclude);
    });
    return !found;
  })
  .map((route) => {
    if (route.name.includes("[tab]")) {
      route.name = "Tab";
    }
    return {
      url: route.path,
      label: route.name.replace("ionic/", ""),
      icon: "home",
    };
  })
  .sort(function (a, b) {
    var nameA = a.label.toUpperCase(); // ignore upper and lowercase
    var nameB = b.label.toUpperCase(); // ignore upper and lowercase
    if (nameA < nameB) {
      return -1;
    }
    if (nameA > nameB) {
      return 1;
    }

    // names must be equal
    return 0;
  });

// randomize the icons for the menu
// using RXJS for fun
let icons;
fromFetch("/assets/json/ionicons.json").subscribe(
  (response) => {
    response.json().then((json) => {
      icons = json.icons;
      menuItems.map((menuItem) => {
        //   menuItem.icon = "at";
        menuItem.icon = icons[Math.floor(Math.random() * icons.length)];
      });
      menuItems = [...menuItems];
    });
  },
  (error) => {
    console.error("Error HTTP", error);
  }
);

const closeAndNavigate = (url) => {
  console.log("Navigate url", url);

  defaultAnalytics.logEvent("page_view", { page_title: url });

  path.set(url);
  $goto(url);

  getIonicMenu("mainmenu")
    .close(true)
    .then(() => {});
};

const goToReview = () => {
  path.set("/RateMe");
  getIonicMenu("mainmenu")
    .close(true)
    .then(() => {});
};

const GITHUBclick = () => {
  defaultAnalytics.logEvent("page_view", { page_title: "GITHUB_go" });
};

const FORUMclick = () => {
  defaultAnalytics.logEvent("page_view", { page_title: "FORUM_go" });
};

// hack because of visibility of menu in Chrome/Windows
setTimeout(() => {
  hideMenu = false;
}, 1000);
</script>
