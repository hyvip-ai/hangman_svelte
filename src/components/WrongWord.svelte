<script>
  export let wrongWords = [];
</script>

<main>
  {#if wrongWords.length}
    <h3>Wrong Words Are :</h3>
    <div>
        {#each wrongWords as word (word)}
            <span>{word}</span>
        {/each}
    </div>
  {:else}
    <h3>No Wrong Words Present Currently</h3>
  {/if}

</main>
<style>
    span{
        display: inline-block;
        padding: 0px 1rem;
        position: relative;
        
    }
    span::after{
        content: '';
        display: block;
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
        border-right: 1px solid;
    }
</style>