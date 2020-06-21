<script>
  import WatchButton from "./WatchButton.svelte";
  import { slide, fade } from "svelte/transition";
  let medias = [];
  let showMedias = [];
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
      medias = call.medias;
      showMedias = medias;
    }
  }

  let searchQuery = "";
  function filter(e) {
    e.preventDefault();

    showMedias = medias.filter(value => {
      return value.name.toLowerCase().indexOf(searchQuery.toLowerCase()) !== -1;
    });
  }
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
    {#if medias.length === 0}
      <h2>Loading...</h2>
    {/if}
    <table>
      {#each showMedias as media, i}
        <tr >
          <td>{media.name}</td>
          <td class="link">
            <WatchButton {i} {media} />
          </td>
        </tr>
      {/each}
    </table>
  </div>
</div>
