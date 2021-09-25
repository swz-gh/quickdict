<script>
  import Word from "./components/Word.svelte";
  let dictData = null;
  let input = "";
  let disabled = false;
  async function lookup() {
    disabled = true;
    let req = await fetch(
      `https://api.dictionaryapi.dev/api/v2/entries/en/${input}`
    ).catch((e) => {
      console.error(e);
      disabled = false;
    });
    if (!req) {
      return (disabled = false);
    }
    dictData = await req.json();
    disabled = false;
  }

  function inputKeyPress() {
    // Number 13 is the "Enter" key on the keyboard
    if (event.keyCode === 13) {
      lookup();
    }
  }
</script>

<main>
  <h1>quickdict</h1>
  <div class="in">
    <input
      type="text"
      placeholder="Internet"
      bind:value={input}
      on:keyup={inputKeyPress}
    />
    <button {disabled} on:click={lookup}
      >{disabled ? "loading..." : "look up"}
    </button>
  </div>
  {#if dictData != null}
    <div class="definitions">
      {#each dictData as word}
        <Word {word} />
      {/each}
    </div>
  {/if}
</main>

<style>
  main {
    background-color: #0f0f0f;
    color: rgb(200, 200, 200);
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  * {
    margin: 0px;
  }
  .in {
    text-align: center;
  }
  input,
  button {
    font-size: x-large;
    background-color: #2f2f2f;
    border: none;
    color: rgb(200, 200, 200);
    border-radius: 0.2rem;
    margin: 0 0.5rem;
  }
  button {
    cursor: pointer;
  }
  button:hover {
    background-color: #3f3f3f;
  }
  button:active {
    background-color: #2e2e2e;
  }
  button:disabled {
    background-color: transparent;
    color: #646464;
    cursor: initial;
  }
  h1 {
    font-size: 4rem;
    font-family: Georgia, "Times New Roman", Times, serif;
    margin-bottom: 0.8rem;
  }
  .definitions {
    overflow-y: scroll;
    margin: 0 1rem;
  }
</style>
