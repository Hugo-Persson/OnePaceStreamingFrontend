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
  <script>
  export let path;
    function copyTheText() {
    /* Select the text field */
    copyText.select();
    copyText.setSelectionRange(0, 99999); /*For mobile devices*/

    /* Copy the text inside the text field */
    document.execCommand("copy");
  }
    let copyText;
  </script>