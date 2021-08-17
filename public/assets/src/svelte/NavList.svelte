<svelte:head>
  <title>Ionic Companion - NavList</title>
</svelte:head>
<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Nav</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content fullscreen>
  <ion-list>
    {#each techs as tech}
      <ion-item
        button
        on:click="{() => {
          showDetail(tech.title);
        }}"
      >
        <ion-icon slot="start" name="{'logo-' + tech.icon}"></ion-icon>
        <ion-label>
          <h3>{tech.title}</h3>
        </ion-label>
      </ion-item>
    {/each}
  </ion-list>
</ion-content>

<script>
import NavDetail from "./NavDetail.svelte";
import { techs } from "./techs.js";
import {
  registerWebComponentOnce,
  getIonicNav,
  getIonicMenu,
} from "../../services/IonicControllers";

registerWebComponentOnce("nav-detail", NavDetail);

const nav = getIonicNav();

function showDetail(title) {
  const tech = techs.find((tech) => tech.title === title);
  nav.push("nav-detail", { tech });
}

function openMenu() {
  getIonicMenu("mainmenu").open();
}
</script>
