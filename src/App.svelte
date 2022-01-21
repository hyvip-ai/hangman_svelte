<script>
  import GameOver from "./components/GameOver.svelte";
  import { onMount } from "svelte";
  import HangMan from "./components/HangMan.svelte";
  import Life from "./components/Life.svelte";
  import WrongWord from "./components/WrongWord.svelte";
  import CorrectWord from "./components/CorrectWord.svelte";
  import Loader from "./components/Loader.svelte";
  import Win from "./components/Win.svelte";
  let mainWord = "";
  let wrongWords = [];
  let win = false;
  $: correctWords = mainWord.split("");
  $: enteredWords = [
    correctWords[Math.floor(correctWords.length * Math.random())],
  ];
  let lifeCount = 5;
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
  const checkWin = () => {
    return mainWord.split("").every((item) => {
      return enteredWords.includes(item);
    });
  };
  window.addEventListener("keyup", (e) => {
    const { key, keyCode } = e;
    if (keyCode >= 65 && keyCode <= 90) {
      if (correctWords.includes(key)) {
        if (enteredWords.includes(key)) {
          alert("The word is already entered try soemthing else moron !!!!");
        } else {
          enteredWords = [key, ...enteredWords];
          win = checkWin();
        }
      } else {
        wrongWords = [key, ...wrongWords];
        if (lifeCount > 0) {
          lifeCount -= 1;
        } else {
          gameOver = true;
        }
      }
    }
  });
  const resetGame = async () => {
    win = false;
    gameOver = false;

    setTimeout(async () => {
      loading = true;
      lifeCount = 5;
      correctWords = [];
      wrongWords = [];

      let result = await fetch(
        `https://random-word-api.herokuapp.com/word?number=1`
      );
      let data = await result.json();
      mainWord = data[0];
      loading = false;
    }, 100);
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
    <Win on:win-game={resetGame} {win} />
    {#if correctWords.length}
      <CorrectWord {correctWords} {enteredWords} />
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
