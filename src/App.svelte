<script>
  import data from './lib/movies';

  const handleLike = ({index}) => {
    data[index].likeCount += 1;
  };

  let isModal = false;
  let selectedMovie = 0;
</script>

<main class="container">
  <h1>영화정보</h1>
  {#each data as item, i}
    <div class="item">
      <figure>
        <img src={item.imageUrl} alt={item.title}/>
      </figure>
      <div class="info">
        <h3 class="bg-yellow">{item.title}</h3>
        <p>개봉: {item.year}</p>
        <p>장르: {item.category}</p>
        <button on:click={
                () => {handleLike({index: i})}
            }>좋아요 {item.likeCount}
        </button>
        <button class="btn btn-primary" on:click={() => {
          isModal = true;
          selectedMovie = i;
          }}>상세보기
        </button>
      </div>
    </div>
  {/each}
</main>

{#if isModal}
  <div class="modal">
    <div class="inner">
      <h3>{data[selectedMovie].title}</h3>
      <p>
        {@html data[selectedMovie].story}
      </p>
      <button class="btn-close" on:click={() => isModal = false}>닫기</button>
    </div>
  </div>
{/if}

<style>
  .bg-yellow {
    background-color: gold;
    padding: 10px;
    color: black;
  }

  .item {
    width: 100%;
    border: 1px solid #ccc;
    display: flex;
    margin-bottom: 20px;
    padding: 1rem;
  }

  .item figure {
    width: 30%;
    margin-right: 1rem;
  }

  .item img {
    width: 100%;
  }

  .item .info {
    width: 100%;
  }

  .modal {
    background: rgba(0, 0, 0, 0.7);
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal .inner {
    background: #fff;
    width: 80%;
    padding: 20px;
    border-radius: 10px;
  }
</style>
