<script>
  export let data_temp = [];
  export let openModal;
  export let handleLike;
</script>

<main>
  <h1>영화정보</h1>
  {#each data_temp as item, i}
    <div class="item">
      <figure>
        <img src={item.imageUrl} alt={item.title}/>
      </figure>
      <div class="info">
        <h3 class="bg-yellow">{item.title}</h3>
        <p>개봉: {item.year}</p>
        <p>장르: {item.category}</p>
        <button on:click={
                () => {handleLike(item.id)}
            }>좋아요 {item.likeCount}
        </button>
        <button class="btn btn-primary" on:click={
          () => {
            openModal(item.id);
          }}>상세보기
        </button>
      </div>
    </div>
  {/each}
</main>

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
</style>