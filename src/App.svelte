<script>
  export let name;
  import { slide, fade } from "svelte/transition";
  import { medias } from "./medias.js";
  import PickMedia from "./PickMedia.svelte";
  import StreamSite from "./StreamSite.svelte";

  let page = "";

  let path = "";
  let mediaName;
  let index;
  onhashchange = directPage;
  directPage();
  function directPage() {
    const dataArray = location.hash.split("&");
    page = dataArray[1];
    index = dataArray[2];
    path = "http://" + location.host + "/stream/" + dataArray[2];
    mediaName = dataArray[3];
    console.log(path);
  }

  getMedias();
  async function getMedias() {
    console.log("H");
    let call = await fetch("http://localhost:8000/getMedias", {
      method: "POST"
    });
    console.log("DONE");
    call = await call.json();
    console.log(call);
    if (call.error) {
    } else {
      medias.set(call.medias);
      console.log("medias", $medias);
    }
  }
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
  #guide {
    text-align: left;
  }
</style>

{#if page == 'watch'}
  <StreamSite {index} {path} {mediaName} />
{:else}
  <PickMedia />
{/if}
