<script>
  import GameOver from "./components/GameOver.svelte";
  import { onMount } from "svelte";
  import HangMan from "./components/HangMan.svelte";
  import Life from "./components/Life.svelte";
  import WrongWord from "./components/WrongWord.svelte";
  import CorrectWord from "./components/CorrectWord.svelte";
  import Loader from "./components/Loader.svelte";
  let mainWord = "";
  let wrongWords = [];
  $: correctWords = mainWord.split("");
  let lifeCount = 7;
  let gameOver = false;
  let loading = true;
  onMount(async () => {
    let result = await fetch(
      `https://random-word-api.herokuapp.com/word?number=1`
    );
    let data = await result.json();
    mainWord = data[0];
    loading = false;
  });
  window.addEventListener("keyup", (e) => {
    const { key, keyCode } = e;
    if (keyCode >= 65 && keyCode <= 90) {
      console.log(key);
      if (lifeCount > 0) {
        lifeCount -= 1;
      } else {
        gameOver = true;
      }
    }
  });
  const resetGame = () => {
    lifeCount = 7;
    correctWords = [];
    wrongWords = [];
    gameOver = false;
  };
</script>

<main>
  {#if loading}
    <Loader />
  {:else}
    <h1>Welcome To Hangman Game !</h1>
    <HangMan {wrongWords} />
    <WrongWord {wrongWords} />
    <Life {lifeCount} />
    <GameOver {gameOver} on:start-new-game={resetGame} />
    {#if correctWords.length}
      <CorrectWord {correctWords} />
    {/if}
  {/if}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 100;
  }
</style>
