<script>
  import WatchButton from "./WatchButton.svelte";
  import { slide, fade } from "svelte/transition";
  import { medias } from "./medias.js";

  let mediaVal = [];
  let showMedias = mediaVal;

  let searchQuery = "";

  medias.subscribe(val => {
    mediaVal = val;
    showMedias = val;
    console.log("VALUY", val);
  });

  function filter(e) {
    e.preventDefault();

    showMedias = mediaVal.filter(value => {
      return value.name.toLowerCase().indexOf(searchQuery.toLowerCase()) !== -1;
    });
  }
  console.log("meeee", $medias);
</script>

<style>
  #container {
    height: 100vh;
    width: 100vw;
    display: grid;
    grid-template-rows: 6% 94%;
    grid-template-columns: 100%;
  }
  #media {
    overflow-y: scroll;
    overflow-x: hidden;

    background-color: #212121;
    color: white;
  }
  #navbar {
    padding: 10px;
    text-align: center;
    display: grid;
    grid-template-columns: 25% 50% 25%;
    background-color: #2e2e2e;
  }
  tr:nth-child(even) {
    background-color: #2e2e2e;
  }
  tr:nth-child(odd) {
    background-color: #212121;
  }
  tr {
    padding: 30px;
  }
  table {
    margin: 0;
    width: 100%;
    line-height: 250%;
  }
  input {
    width: 100%;
  }
  .link {
    text-align: center;
  }
</style>

<div id="container">
  <div id="navbar">
    <div />
    <form on:submit={filter}>
      <input
        class="form-control "
        type="search"
        placeholder="Search"
        aria-label="Search"
        bind:value={searchQuery} />
    </form>

  </div>

  <div id="media">
    {#if mediaVal.length === 0}
      <h2>Loading...</h2>
    {/if}
    <table>
      {#each showMedias as media, i}
        <tr transition:fade>
          <td>{media.name}</td>
          <td class="link">
            <WatchButton {i} {media} />
          </td>
        </tr>
      {/each}
    </table>
  </div>
</div>
