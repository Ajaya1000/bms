<script>
  let data = [1, 2, 3, 4, 5];
  import InfiniteScrollTest from "./lib/InfiniteScrollTest.svelte";

  let hasNext;
  let hasPrev;
  const loadNext = (event) => {
    console.log(event);
  };
  const loadPrev = (event) => {
    console.log(event);
  };
</script>

<svelte:head>
  <title>BookMyShoot</title>
</svelte:head>

<main>
  <InfiniteScrollTest
    {hasNext}
    {hasPrev}
    on:loadNext={loadNext}
    on:loadPrev={loadPrev}>
    {#each data as item}
      <h3>item</h3>
    {/each}
  </InfiniteScrollTest>
</main>
