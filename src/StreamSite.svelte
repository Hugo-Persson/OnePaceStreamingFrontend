<script>
  export let mediaName;
  export let path;
  export let index;

  import { medias } from "./medias.js";
  function copyTheText() {
    /* Select the text field */
    copyText.select();
    copyText.setSelectionRange(0, 99999); /*For mobile devices*/

    /* Copy the text inside the text field */
    document.execCommand("copy");
  }
  let copyText;

  function nextEpisode() {
    //TODO: Account for last episode
    index = new Number(index);
    const newIndex = index + 1;
    console.log("INDEX", index + 1);
    const media = $medias[newIndex];
    const newPath = `#&watch&${newIndex}&${media.name}`;
    location.hash = newPath;
  }
  function previousEpisode() {
    index = new Number(index);
    const media = $medias[index - 1];
    const newPath = `#&watch&${index - 1}&${media.name}`;
    location.hash = newPath;
  }
</script>

<style>
  main {
    color: white;
  }
  #top {
    text-align: center;
    margin-bottom: 50px;
  }
  input {
    width: 40%;
  }
  #navigation {
    display: grid;
    grid-template-columns: 10% 15% 60% 15%;
    align-items: center;
  }
  #navigation div {
    text-align: left;
  }
  #prev {
    text-align: right !important;
  }
</style>

<main>
  <div id="top">

    <div id="navigation">
      <a href="#">Return to media picker</a>
      <div id="prev">
        <button on:click={previousEpisode}>Previous</button>
      </div>

      <h1>{mediaName.replace(new RegExp('%20', 'g'), ' ')}</h1>
      <div>
        <button on:click={nextEpisode}>Next</button>
      </div>

    </div>

    <input type="text" readonly bind:value={path} bind:this={copyText} />
    <button type="button" on:click={copyTheText}>Copy</button>
  </div>

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
