<svelte:head>
  <title>Ionic Companion - Tabs-Games</title>
</svelte:head>
<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Games</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content fullscreen>
  <ion-button expand="full" color="secondary" on:click="{showDetail}">
    Open a detail nav with back button.
  </ion-button>
  This is not working. Issue is that the Nav and the Tabs are not working nicely
  together. We need an ion-nav element to do the push. So not resolved yet....
</ion-content>

<script>
import AltDetails from "./AltDetails.svelte";
import { onMount } from "svelte";
import { techs } from "./techs.js";
import {
  registerWebComponentOnce,
  getIonicNav,
} from "../../services/IonicControllers";

// not the proper one - as a nav in a tab is a difficult thing
registerWebComponentOnce("nav-detail", AltDetails);

let nav;
onMount(() => {
  nav = getIonicNav();
  console.log("NAV", nav);
});

function showDetail() {
  const title = "Tux";
  const tech = techs.find((tech) => tech.title === title);
  console.log("navpush", tech);
  nav.push("nav-detail", { tech });

  // navigate("/navdetails/" + title);
}
</script>
