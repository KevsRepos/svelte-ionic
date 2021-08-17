<svelte:head>
  <title>Ionic Companion - Avatars</title>
</svelte:head>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Avatar</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content fullscreen>
  <ion-list-header>Default</ion-list-header>
  <ion-avatar class="ion-margin-start">
    <img alt="avatar" src="../assets/img/ionic/avatar.svg" />
  </ion-avatar>

  <ion-list-header>Chip Avatar</ion-list-header>
  <ion-chip class="ion-margin-start">
    <ion-avatar>
      <img alt="avatar" src="../assets/img/ionic/avatar.svg" />
    </ion-avatar>
    <ion-label>Kit Bishop</ion-label>
  </ion-chip>

  <ion-list>
    <ion-list-header>Item Avatars</ion-list-header>
    <ion-item>
      <ion-avatar slot="start">
        <img alt="avatar" src="../assets/img/ionic/avatar.svg" />
      </ion-avatar>
      <ion-label>Lorem ipsum</ion-label>
    </ion-item>
    <ion-item on:click="{startAnimation}" bind:this="{avatar}">
      <ion-avatar slot="end">
        <img alt="avatar" src="../assets/img/ionic/avatar.svg" />
      </ion-avatar>
      <ion-label>
        <h3>Click me!</h3>
        <p>Click this item to launch the WEB Animation API</p>
      </ion-label>
    </ion-item>
    <ion-item>
      <ion-avatar slot="start">
        <img alt="avatar" src="../assets/img/ionic/avatar.svg" />
      </ion-avatar>
      <ion-label>
        <h3>Lorem ipsum</h3>
        <p>dolor sit amet</p>
      </ion-label>
    </ion-item>
    <ion-item>
      <ion-avatar slot="start">
        <img alt="avatar" src="../assets/img/ionic/avatar.svg" />
      </ion-avatar>
      <ion-label>
        <h3>Lorem ipsum</h3>
        <p>dolor sit amet</p>
        <p>consectetur adipiscing elit. Duis ut urna neque.</p>
      </ion-label>
    </ion-item>
    <ion-item>
      <ion-avatar slot="end">
        <img alt="avatar" src="../assets/img/ionic/avatar.svg" />
      </ion-avatar>
      <ion-label>Lorem ipsum</ion-label>
    </ion-item>
    <ion-item>
      <ion-avatar slot="end">
        <img alt="avatar" src="../assets/img/ionic/avatar.svg" />
      </ion-avatar>
      <ion-label>
        <h3>Lorem ipsum</h3>
        <p>dolor sit amet</p>
      </ion-label>
    </ion-item>
  </ion-list>

  <br />

  <ion-card class="stories-card" scroll-x="true">
    <ion-list lines="none" class="story-list">
      {#each avatars as { name, src }, i}
        <ion-item lines="none" class="story-item">
          <ion-avatar class="story-avatar">
            <img class="story-img" alt="{name}" src="{src}" />
          </ion-avatar>
        </ion-item>
        <div class="story-author">
          <ion-text color="primary">{name}</ion-text>
        </div>
      {/each}
    </ion-list>
  </ion-card>
  Scroll me vertically (not implemented correctly) <br /> Courtesy : https://github.com/thenaim/ionic-tk-social-network
  <br /> https://s3.amazonaws.com/uifaces/faces/twitter/yayteejay/128.jpg
</ion-content>

<style>
.story-avatar {
  background: blue;
  height: 64px;
  width: 64px;
  padding: 2px;
  margin-top: 0px;
  margin-bottom: 0px;
}

.story-img {
  border: 2px solid white;
  border-radius: 50%;
}

.story-list {
  padding-top: 0px;
  padding-bottom: 0px;
}

.story-item {
  --inner-padding-bottom: 0px;
  --inner-padding-end: 0px;
  --inner-padding-start: 0px;
  --inner-padding-top: 0px;
  --padding-end: 0px;
  --padding-start: 0px;

  margin: 8px;
  transition: all 0.1s ease-in-out;
}
.story-item:active {
  transform: scale(11.1);
}

.story-author {
  text-align: center;
  margin-bottom: var(--ion-margin, 8px);
}

.stories-card {
  margin: 0px;
  margin-top: var(--ion-margin, 16px);
  border-radius: 0px;
}

.scrollX {
  display: flex;
  flex-wrap: nowrap;
  overflow-x: auto;
  -ms-overflow-style: none;
  flex: 0 0 auto;
}

.scrollX::-webkit-scrollbar {
  display: none;
}
</style>

<script>
import { onMount } from "svelte";
import { IonicShowToast } from "./../../services/IonicControllers";

// https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Using_the_Web_Animations_API
const aliceTiming = {
  duration: 7000,
};

const aliceTumbling = [
  { transform: "rotate(0) scale(1)", color: "#000" },
  { transform: "rotate(360deg) scale(0.1)", color: "#000" },
  { transform: "rotate(0) scale(1)", color: "#000" },
];

let avatar;
const startAnimation = () => {
  if (!avatar.animate) {
    IonicShowToast({
      color: "danger",
      duration: 4000,
      message: "Web Animations API not available",
      showCloseButton: true,
    });
  } else {
    avatar.animate(aliceTumbling, aliceTiming);
  }
};

const avatars = [
  { name: "Ben", src: "../assets/img/ionic/avatar-ben.png" },
  { name: "Finn", src: "../assets/img/ionic/avatar-finn.png" },
  { name: "Leia", src: "../assets/img/ionic/avatar-leia.png" },
  { name: "Rey", src: "../assets/img/ionic/avatar-rey.png" },
  { name: "Yoda", src: "../assets/img/ionic/avatar-yoda.png" },
  { name: "Poe", src: "../assets/img/ionic/avatar-poe.png" },
  { name: "Han", src: "../assets/img/ionic/avatar-han.png" },
  { name: "Luke", src: "../assets/img/ionic/avatar-luke.png" },
];
</script>
