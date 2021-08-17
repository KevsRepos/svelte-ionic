<svelte:head>
  <title>Ionic Companion - Pane - experimental</title>
</svelte:head>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Pane</ion-title>
  </ion-toolbar>
</ion-header>
<ion-content padding scroll-y="false">
  <h1>Cupertino Pane</h1>
  <ion-text>
    <p>
      Cupertino Pane is great modern slide-over pane with touch technologies.
    </p>
    <p>
      Right like in Apple Maps, Apple Stocks, Apple Music and other modern apps.
      Lightweight, Multiplatform, Open Source. For progressive applications.
    </p>
    <br /> Repo: <a
      href="https://github.com/roman-rr/cupertino-pane"
      target="_blank"
    >
      roman-rr/cupertino-pane
    </a>
  </ion-text>

  <div class="cupertino-pane">
    <div class="cupertino-header">
      <h1>Drag me up!</h1>
    </div>
    <div class="cupertino-content">
      <ion-text color="primary">
        <h1>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h1>
      </ion-text>

      <ion-text color="secondary">
        <h2>Nam rutrum justo massa, maximus elementum leo dignissim ac.</h2>
      </ion-text>

      <ion-text color="tertiary">
        <h3>Vestibulum eleifend lorem nec neque interdum varius.</h3>
      </ion-text>

      <ion-text color="success">
        <h4>Sed in neque at nibh congue tincidunt.</h4>
      </ion-text>

      <ion-text color="warning">
        <h5>
          Vestibulum ante ipsum primis in faucibus orci luctus et ultrices
          posuere cubilia Curae;
        </h5>
      </ion-text>

      <ion-text color="danger">
        <h6>Suspendisse potenti.</h6>
      </ion-text>

      <p>
        Donec magna odio,
        <ion-text color="primary">semper</ion-text>
        ac nibh et, vestibulum eleifend felis. Donec
        <ion-text color="secondary">pulvinar</ion-text>
        ex non quam vulputate malesuada in a magna. Praesent massa arcu,
        <ion-text color="tertiary">vehicula</ion-text>
        id pharetra et, cursus at lectus.
      </p>
    </div>
  </div>
</ion-content>

<style>
.cupertino-header,
.cupertino-content {
  margin: 20px;
}
</style>

<script>
//
// https://github.com/roman-rr/cupertino-pane
//
import { CupertinoPane } from "cupertino-pane";

import { onMount } from "svelte";

onMount(() => {
  var myPane = new CupertinoPane(
    ".cupertino-pane", // Pane container selector
    {
      onDrag: () => console.log("Drag event"),
      breaks: {
        top: { enabled: true, offset: -10 },
        middle: { enabled: true, offset: 180 },
        bottom: { enabled: true, offset: 140 },
      },
    }
  );
  myPane.present();
});
</script>
