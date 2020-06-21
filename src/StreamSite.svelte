<script>
  export let mediaName;
  export let path;
  function copyTheText() {
    /* Select the text field */
    copyText.select();
    copyText.setSelectionRange(0, 99999); /*For mobile devices*/

    /* Copy the text inside the text field */
    document.execCommand("copy");
  }
  let copyText;

  function nextEpisode() {}
  function previousEpisode() {}
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
    grid-template-columns: 20% 60% 20%;
    align-items: center;
  }
  #navigation div {
    text-align: left;
  }
  #navigation div:first-of-type {
    text-align: right;
  }
</style>

<main>
  <div id="top">
    <div id="navigation">
      <div>
        <button>Previous</button>
      </div>

      <h1>{mediaName.replace(new RegExp('%20', 'g'), ' ')}</h1>
      <div>
        <button>Next</button>
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
