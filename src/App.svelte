<script>
  const data = [
    {
      title: "고질라 X 콩: 뉴 엠파이어",
      year: 2024,
      category: "어드벤처, 액션, SF",
      likeCount: 0,
    },
    {
      title: "듄: 파트2",
      year: 2024,
      category: "액션",
      likeCount: 0,
    }
  ];

  const handleLike = ({index}) => {
    data[index].likeCount += 1;
  };
</script>

<main>
    <h1>영화정보</h1>
    {#each data as item, i}
        <div>
            <h3 class="bg-yellow">{item.title}</h3>
            <p>개봉: {item.year}</p>
            <p>장르: {item.category}</p>
            <button on:click={
                () => {handleLike({index: i})}
            }>좋아요 {item.likeCount}</button>
        </div>
    {/each}
</main>

<style>
    .bg-yellow {
        background-color: gold;
        padding: 10px;
        color: black;
    }
</style>
