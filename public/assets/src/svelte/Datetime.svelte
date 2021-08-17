<svelte:head>
  <title>Ionic Companion - Datetime</title>
</svelte:head>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>DateTime</ion-title>
  </ion-toolbar>
</ion-header>
,
<ion-content fullscreen>
  <ion-list>
    <ion-item>
      <ion-input placeholder="Title"></ion-input>
    </ion-item>
    <ion-item>
      <ion-input placeholder="Location"></ion-input>
    </ion-item>
    <ion-item-divider></ion-item-divider>
    <ion-item>
      <ion-label>Start Date</ion-label>
      <ion-datetime
        on:ionChange="{changeValue}"
        value="1990-02-19"
        placeholder="Select Date"
      ></ion-datetime>
    </ion-item>
    <ion-item>
      <ion-label>Start Time</ion-label>
      <ion-datetime
        on:ionChange="{changeValue}"
        display-format="h:mm A"
        picker-format="h:mm A"
        value="1990-02-19T07:43Z"
      ></ion-datetime>
    </ion-item>
    <ion-item>
      <ion-label>Ends</ion-label>
      <ion-datetime
        on:ionChange="{changeValue}"
        value="1990-02-20"
        placeholder="Select Date"
      ></ion-datetime>
    </ion-item>
    <ion-item>
      <ion-label>Repeat</ion-label>
      <ion-datetime placeholder="Never" disabled></ion-datetime>
    </ion-item>
    <ion-item>
      <ion-label>Travel Time</ion-label>
      <ion-datetime placeholder="None" disabled></ion-datetime>
    </ion-item>
    <ion-item-divider></ion-item-divider>
    <ion-item>
      <ion-label>Alert</ion-label>
      <ion-datetime placeholder="None" disabled></ion-datetime>
    </ion-item>
  </ion-list>
</ion-content>

<script>
const changeValue = (event) => {
  console.log("Change of value", event.detail);
};
</script>
