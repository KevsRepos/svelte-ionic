<svelte:head>
  <title>Ionic Companion - Refresher</title>
</svelte:head>
<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Pull to refresh</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content>
  <ion-refresher
    slot="fixed"
    bind:this="{refresher}"
    on:ionRefresh="{refreshAction}"
  >
    <ion-refresher-content></ion-refresher-content>
  </ion-refresher>

  <ion-list bind:this="{list}"></ion-list>
</ion-content>

<style>
:root {
  --ion-safe-area-top: 20px;
  --ion-safe-area-bottom: 22px;
}
ion-content {
  user-select: none;
}
ion-item {
  --padding-start: 8px;
}
.unread {
  width: 10px;
  height: 10px;
  border-radius: 10px;
  background-color: #3684ff;
  margin-top: 15px;
  margin-right: 8px;
  align-self: start;
}
ion-item h2 {
  font-weight: 500 !important;
}
ion-item h3 {
  color: #777;
}
</style>

<script>
import { onMount } from "svelte";
const names = [
  "Burt Bear",
  "Charlie Cheetah",
  "Donald Duck",
  "Eva Eagle",
  "Ellie Elephant",
  "Gino Giraffe",
  "Isabella Iguana",
  "Karl Kitten",
  "Lionel Lion",
  "Molly Mouse",
  "Paul Puppy",
  "Rachel Rabbit",
  "Ted Turtle",
];

let list;
let refresher;

const refreshAction = () => {
  console.log("Refresh action");
  setTimeout(() => {
    prependMessages(5, true);
    refresher.complete();
  }, 2000);
};

onMount(() => {
  appendMessages(5, false);
});

function chooseRandomName() {
  return names[Math.floor(Math.random() * names.length)];
}
function appendMessages(numMessages = 1, unread) {
  for (let i = 0; i < numMessages; i++) {
    list.appendChild(createMessage(unread, i));
  }
}
function prependMessages(numMessages = 1, unread) {
  for (let i = 0; i < numMessages; i++) {
    list.insertBefore(createMessage(unread, i), list.firstChild);
  }
}
function createMessage(unread = false, i = 1) {
  let item = document.createElement("ion-item");
  const ran = i;
  item.innerHTML = `
        <div slot="start" class="${unread ? "unread" : "read"}"></div>
        <ion-avatar slot="start">
            <img src="https://www.gravatar.com/avatar/${ran}?d=monsterid&f=y">
          </ion-avatar>
        <ion-label class="ion-text-wrap">
          <h2>${chooseRandomName()}</h2>
          <h3>Lorem ipsum dolor sit amet, consectetur adipiscing elit</h3>
        </ion-label>
      `;
  return item;
}
</script>
