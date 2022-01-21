<script>
  import { scale } from "svelte/transition";
  export let lifeCount = 0;
  $: lifeCountArray = [...Array(lifeCount).keys()];
</script>

<main>
  <h3>Life Reamining</h3>
  {#if lifeCount === 0}
    <p>Last Chance</p>
  {/if}
  {#each lifeCountArray as life (life)}
    <div transition:scale>
      <i class="fas fa-heart" />
    </div>
  {/each}
</main>

<style>
  div {
    display: inline-block;
  }
  i {
    display: inline-block;
    margin: 0px 1rem;
  }
</style>
