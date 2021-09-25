<script>
  export let word;
</script>

<div class="word">
  <div class="title">
    <h1>{word.word}</h1>
    {#each word.phonetics as pho}
      <a href={pho.audio ?? "#"}><h4>{pho.text ?? ""}</h4></a>
    {/each}
  </div>
  {#if word.origin != undefined}
    <div class="origin leftm">
      <h2>origin</h2>
      <p>{word.origin}</p>
    </div>
  {/if}
  <div class="meanings leftm">
    {#each word.meanings as mng}
      <h3>{mng.partOfSpeech}</h3>
      {#each mng.definitions as defi}
        <p class="def leftm">{defi.definition}</p>
        {#if defi.example != undefined}
          <p class="ex leftm"><strong>example:</strong> {defi.example}</p>
        {/if}
      {/each}
    {/each}
  </div>
</div>

<style>
  .title {
    display: flex;
    align-items: center;
  }
  .title h1 {
    text-decoration: underline;
  }
  .title * {
    margin: 0.2rem;
  }
  a {
    text-decoration: none;
    color: inherit;
  }
  .origin h2 {
    margin: 0px;
  }
  .leftm {
    margin-left: 2rem;
  }
  .def {
    margin-top: 0px;
    margin-bottom: 0px;
  }
  .ex {
    margin-top: 0px;
  }
  @media (orientation: landscape) {
    .word {
      max-width: 70vw;
    }
  }
</style>
