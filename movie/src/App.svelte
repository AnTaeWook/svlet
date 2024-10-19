<script>
  import data from './lib/movies';
  import Navbar from './lib/components/Navbar.svelte';
  import Modal from './lib/components/Modal.svelte';
  import Movies from './lib/components/Movies.svelte';
  import Event from "./lib/components/Event.svelte";
  import SearchBar from "./lib/components/SearchBar.svelte";
  import {onDestroy, onMount} from "svelte";

  const eventText = [
    "NETPLIX 강렬한 운명의 드라마, 경기크리처",
    "NETPLIX 미스터리 스릴러, 더 블랙리스트",
    "NETPLIX 로맨틱 코미디, 브리짓 존스의 일기",
  ]

  let data_temp = [...data];

  const handleLike = (id) => {
    data.map(movie => {
      if (movie.id === id) {
        movie.likeCount++;
      }
    });
    data_temp = data.filter(movie => {
      return data_temp.includes(movie);
    })
  };

  let isModal = false;
  let selectedMovie = {};

  const closeModal = () => {
    isModal = false;
  }
  const openModal = (i) => {
    isModal = true;
    selectedMovie = data.find(movie => movie.id === i);
  }

  let isEvent = true;
  const closeEvent = () => {
    isEvent = false;
  }

  let alertText = ""
  let eventIndex = 0;
  let intervalEventId;

  onMount(() => {
    intervalEventId = setInterval(() => {
      eventIndex++;
      console.log("interval event")
    }, 3000);
  });
</script>

<Navbar/>

{#if isEvent}
  <Event
      {closeEvent}
      {eventText}
      {eventIndex}
      {intervalEventId}
  />
{/if}

<SearchBar
    {data}
    bind:data_temp
    bind:alertText
/>

<div class="container">
  <button on:click={() => {
  data_temp = [...data];
  alertText = ""
}}>전체보기</button>
</div>

<Movies
    {data_temp}
    {openModal}
    {handleLike}
/>

{#if isModal}
  <Modal
      {selectedMovie}
      {closeModal}
  />
{/if}

<style>
  .container {
    text-align: center;
  }
</style>
