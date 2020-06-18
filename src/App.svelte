<script>
  export let name;

  import PickMedia from "./PickMedia.svelte";
  import StreamSite from "./StreamSite.svelte";

  let page = "";

  let path = "";

  onhashchange = directPage;
  directPage();
  function directPage() {
    const dataArray = location.hash.split("&");
    page = dataArray[1];
    path = "http://" + location.host + "/stream/" + dataArray[2];
    console.log(path);
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
  <StreamSite {path} />
{:else}
  <PickMedia />
{/if}
