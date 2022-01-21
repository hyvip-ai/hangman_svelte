<script>
  import { v4 as uuid } from "uuid";
  export let correctWords = [];
  export let enteredWords = [];
  console.log(correctWords);
</script>

<main>
  <h3>Correct Letters Will Appear Hear</h3>
  {#each correctWords as word (uuid())}
    {#if enteredWords.includes(word)}
      <span>{word}</span>
    {:else}
      <span>_</span>
    {/if}
  {/each}
</main>

<style>
  span {
    display: inline-block;
    margin: 0px 1rem;
    font-size: 20px;
  }
</style>
