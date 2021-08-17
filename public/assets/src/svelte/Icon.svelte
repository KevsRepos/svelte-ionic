<svelte:head>
  <title>Ionic Companion - Icons</title>
</svelte:head>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-title>Icons</ion-title>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
  </ion-toolbar>
  <ion-toolbar>
    <ion-searchbar
      show-cancel-button="'never'"
      bind:this="{searchBar}"
    ></ion-searchbar>
  </ion-toolbar>
</ion-header>

<ion-content fullscreen class="ion-padding">
  <ion-grid>
    <ion-row>
      {#each list as icon}
        <ion-col
          on:click="{() => {
            iconClicked(icon);
          }}"
        >
          <ion-icon name="{icon}" color="{getRandomColor()}"></ion-icon>
        </ion-col>
      {/each}
    </ion-row>
  </ion-grid>
</ion-content>

<style>
ion-icon {
  font-size: 500%;
}
</style>

<script>
import { fromFetch } from "rxjs/fetch";
import { Plugins } from "@capacitor/core";
import { IonicShowToast } from "../../services/IonicControllers";

import { fromEvent } from "rxjs";
import { onMount } from "svelte";
import {
  map,
  filter,
  debounceTime,
  distinctUntilChanged,
} from "rxjs/operators";

let searchBar;
let length = 0;
let icons = [];
let list = [];
let infiniteScroll;
const { Clipboard } = Plugins;

// let's get the icons
fromFetch("/assets/json/ionicons.json").subscribe(
  (response) => {
    response.json().then((json) => {
      icons = json.icons;
      console.log("List of icons", icons);

      // icons = icons.slice(0, 100); // for debugging
      list = icons.slice(0, 300);
      // we delay the full display to smoothen the rendering
      setTimeout(() => {
        list = [].concat(icons);
      }, 3000);
    });
  },
  (error) => {
    console.error("Error HTTP", error);
  }
);

const iconClicked = (icon) => {
  console.log("Icon clicked", icon);

  Clipboard.write({
    string: `<ion-icon name="${icon}"></ion-icon>`,
  });
  IonicShowToast({
    color: "dark",
    duration: 3000,
    message: `<ion-icon style="font-size:350%" name="${icon}"></ion-icon> - ${icon}`,
    showCloseButton: true,
  });
};

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

onMount(() => {
  // not firing when the cancel button is clicked - unsure why the cancel button is shown at all!
  fromEvent(searchBar, "input")
    .pipe(
      // get value
      map((event) => {
        console.log("INPUT", event);
        return event.target.value;
      }),
      // if character length greater then 2 - removed
      //  filter(res => res.length > 2),

      // Time in milliseconds between key events
      debounceTime(1000),

      // If previous query is diffent from current
      distinctUntilChanged()

      // subscription for response
    )
    .subscribe((text) => {
      const query = text.toLowerCase();
      if (query != "") {
        list = [];
        list = icons.filter((icon) => icon.toLowerCase().indexOf(query) > -1);
      } else {
        list = [].concat(icons);
      }

      console.log("Changing the list ", text, list);
    });
});
</script>
