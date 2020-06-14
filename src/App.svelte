<script>
  export let name;

  let medias = [];
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
    }
  }

  let page = "";

  let path = "";

  let copyText;
  onhashchange = directPage;
  directPage();
  function directPage() {
    const dataArray = location.hash.split("&");
    page = dataArray[1];
    path = "http://" + location.host + "/stream/" + dataArray[2];
    console.log(path);
  }
  function copyTheText() {
    /* Select the text field */
    copyText.select();
    copyText.setSelectionRange(0, 99999); /*For mobile devices*/

    /* Copy the text inside the text field */
    document.execCommand("copy");
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
  <main>
    <h1>Movie time</h1>
    <input type="text" readonly bind:value={path} bind:this={copyText} />
    <button type="button" on:click={copyTheText}>Copy</button>
    <div id="guide">
      <h2>How to open stream</h2>
      <h3>Windows</h3>
      <ul>
        <li>Open vlc player</li>
        <li>Click on media up in the left corner</li>
        <li>Click on open network stream</li>
        <li>Paste url you copied from website</li>
        <li>Click enter/play button</li>
      </ul>
      <h3>Mobile</h3>
      <ul>
        <li>Start app</li>
        <li>Navigate to stream</li>
        <li>Paste url</li>
        <li>Watch</li>
      </ul>
    </div>

  </main>
{:else}
  <main>
    <h1>Select media to stream</h1>
    {#each medias as media, i}
      <div class="media">
        {media.name}
        <br />
        <a href="#&watch&{i}">Watch</a>

        <br />
      </div>
    {/each}
  </main>
{/if}
