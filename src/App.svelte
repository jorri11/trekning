<script lang="ts">
  import Typewriter from "svelte-typewriter";
  import { confetti } from "@neoconfetti/svelte";
  function onClick(e): void {
    isStarted = true;
  }
  let isDone = false;
  let doneTimes = 0;
  function onDone() {
    if (++doneTimes == phrases.length) {
      isDone = true;
    }
  }
  let headerText = "HVEM FÅR VÆRE MED PÅ KONSERT?";
  let isStarted = false;
  const phrases = [
    "1 desember",
    "kulturhuset",
    "konsert",
    "kultur",
    "kokain",
    "nei, ikke kokain",
    "hvem vant trekningen?",
    "nå tenker jeg dere lurer",
    "*intens trommevirvel*",
    "det er Andreas!",
  ];
</script>

<main>
  {#if !isStarted}
    <h1>{headerText}</h1>
    <button type="button" on:click|preventDefault={onClick}
      >Trykk på meg for å sjå</button
    >
  {:else}
    {#if isDone}
      <div use:confetti />
    {/if}
    <Typewriter mode="loopOnce" unwriteInterval={0} on:done={onDone}>
      {#each phrases as phrase}
        <h1>{phrase}</h1>
      {/each}
    </Typewriter>
  {/if}
</main>

<style>
  :global(body) {
    background-color: black;
    color: gray;
    overflow: hidden;
  }
  h1 {
    font-weight: 700;
    text-transform: uppercase;
    font-size: 40px;
  }
  button {
    background: none;
    border: none;
    color: gray;
    padding: 0;
  }
  button:focus {
    border: none;
    outline: none;
  }
</style>
