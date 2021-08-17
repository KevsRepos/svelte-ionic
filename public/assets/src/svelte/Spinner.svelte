<svelte:head>
  <title>Ionic Companion - Spinner</title>
</svelte:head>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Spinner</ion-title>
  </ion-toolbar>
</ion-header>
<ion-content>
  <ion-list>
    <ion-item>
      <ion-label>Default</ion-label>
      <ion-spinner></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Lines</ion-label>
      <ion-spinner name="lines"></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Lines Small</ion-label>
      <ion-spinner name="lines-small"></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Dots</ion-label>
      <ion-spinner name="dots"></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Bubbles</ion-label>
      <ion-spinner name="bubbles"></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Circles</ion-label>
      <ion-spinner name="circles"></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Crescent</ion-label>
      <ion-spinner name="crescent"></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Paused</ion-label>
      <ion-spinner paused></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Primary</ion-label>
      <ion-spinner color="primary"></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Secondary</ion-label>
      <ion-spinner color="secondary"></ion-spinner>
    </ion-item>

    <ion-item>
      <ion-label>Tertiary</ion-label>
      <ion-spinner color="tertiary"></ion-spinner>
    </ion-item>
  </ion-list>
</ion-content>
