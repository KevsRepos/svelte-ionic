<svelte:head>
  <title>Ionic Companion - Checkboxes</title>
</svelte:head>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Checkbox</ion-title>
  </ion-toolbar>
</ion-header>
<ion-content fullscreen>
  <ion-list>
    <ion-list-header>Characters</ion-list-header>
    <ion-item>
      <ion-label>Jon Snow</ion-label>
      <ion-checkbox
        value="jon"
        color="primary"
        checked
        slot="start"
        on:ionChange="{checkBoxChange}"
      ></ion-checkbox>
    </ion-item>
    <ion-item>
      <ion-checkbox
        value="daenerys"
        on:ionChange="{checkBoxChange}"
        color="dark"
        checked
        slot="start"
      ></ion-checkbox>
      <ion-label>Daenerys Targaryen</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox disabled slot="start"></ion-checkbox>
      <ion-label>Arya Stark</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox
        value="tyrion"
        on:ionChange="{checkBoxChange}"
        color="secondary"
        slot="start"
      ></ion-checkbox>
      <ion-label>Tyrion Lannister</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox
        value="sansa"
        on:ionChange="{checkBoxChange}"
        color="danger"
        checked
        slot="start"
      ></ion-checkbox>
      <ion-label>Sansa Stark</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox
        value="khal"
        on:ionChange="{checkBoxChange}"
        color="primary"
        slot="start"
      ></ion-checkbox>
      <ion-label>Khal Drogo</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox
        value="cersei"
        on:ionChange="{checkBoxChange}"
        color="tertiary"
        checked
        slot="start"
      ></ion-checkbox>
      <ion-label>Cersei Lannister</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox
        color="medium"
        value="stannis"
        on:ionChange="{checkBoxChange}"
        checked
        slot="start"
      ></ion-checkbox>
      <ion-label>Stannis Baratheon</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox color="primary" disabled slot="start"></ion-checkbox>
      <ion-label>Petyr Baelish</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox
        color="dark"
        value="hodor"
        on:ionChange="{checkBoxChange}"
        checked
        slot="start"
      ></ion-checkbox>
      <ion-label>Hodor</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox
        color="secondary"
        value="catelyn"
        on:ionChange="{checkBoxChange}"
        checked
        slot="start"
      ></ion-checkbox>
      <ion-label>Catelyn Stark</ion-label>
    </ion-item>
    <ion-item>
      <ion-checkbox
        value="bronn"
        on:ionChange="{checkBoxChange}"
        color="primary"
        slot="start"
      ></ion-checkbox>
      <ion-label>Bronn</ion-label>
    </ion-item>
  </ion-list>
</ion-content>

<script>
let characters = {};

const checkBoxChange = (event) => {
  if (event.detail.value) {
    characters[event.detail.value] = event.detail.checked;
    console.log(JSON.stringify(characters, null, 2));
  }
};
</script>
