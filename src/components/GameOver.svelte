<script>
  import { scale } from "svelte/transition";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  export let gameOver = false;
  const clickHandler = () => {
    dispatch("start-new-game");
  };
</script>

<div>
  {#if gameOver}
    <main class="backdrop">
      <div class="main_content" transition:scale>
        <p class="message">Game Over, Click the button below to start again</p>
        <button on:click={clickHandler}>Start Again</button>
      </div>
    </main>
  {/if}
</div>

<style>
  .backdrop {
    position: fixed;
    height: 100%;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.8);
    top: 0;
    left: 0;
  }
  .main_content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: white;
    border-radius: 5px;
    padding: 2rem;
    color: black;
  }
  .main_content button {
    display: block;
    padding: 0.8rem;
    border-radius: 5px;
    font-weight: bold;
    margin: 0px auto;
    border: none;
    cursor: pointer;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  }
  .main_content button:active {
    box-shadow: none;
    transform: scale(0.95);
  }
</style>
