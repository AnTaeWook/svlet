<script>
  import { fade } from "svelte/transition";
  import {onDestroy} from "svelte";
  export let closeEvent;
  export let eventText = [];
  export let eventIndex = 0;
  export let intervalEventId

  onDestroy(() => {
    clearInterval(intervalEventId)
    console.log("clear interval")
  })
</script>

<div
    class='event'
    transition:fade
>
  <p>{eventText[eventIndex % eventText.length]}</p>
  <button on:click={closeEvent}>X</button>
</div>

<style>
  .event {
    width: 100%;
    background: #666;
    padding: 5px 1em;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #ffffff;
    text-align: center;
    margin-bottom: 1em;
  }

  .event button {
    padding: 2px;
  }
</style>