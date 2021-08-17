<script>
  import IonTab from "../../../components/IonTab.svelte";

  import Controllers from "../Controllers.svelte";
  import Music from "../Music.svelte";
  import Games from "../Games.svelte";

  export let tab = "movies";

  // too much?
  if (tab == ":tab") {
    tab = "movies";
  }

  const myTabs = [
    { label: "Magic", icon: "videocam", tab: "movies", component: Controllers },
    { label: "Text", icon: "musical-note", tab: "music", component: Music },
    {
      label: "Nothing",
      icon: "logo-game-controller-b",
      tab: "games",
      component: Games
    }
  ];

  console.log("Tabs", tab, myTabs);
</script>

<IonTab tabs={myTabs} selected={tab} />
