<script>
  import { onMount, onDestroy, createEventDispatcher } from "svelte";
  let element;
  let dispatch = createEventDispatcher();
  export let hasNext = true;
  export let hasPrev = true;

  const onScroll = () => {
    let d = element.scrollHeight - element.clientHeight;
    let cw;
    if (d <= 0) cw = 0;
    else cw = element.scrollTop / d;
    if (cw < 0.05 && hasPrev) {
      dispatch("loadPrev");
    } else if (cw > 0.95 && hasNext) {
      dispatch("loadNext");
    }
  };

  onMount(() => {
    element.addEventListener("scroll", onScroll);
    element.addEventListener("resize", onScroll);
  });

  onDestroy(() => {
    element.removeEventListener("scroll", onScroll);
    element.removeEventListener("resize", onScroll);
  });
</script>

<style>
  div {
    border: 5px solid red;
  }
</style>

<div bind:this={element}>
  <!-- on:scroll={onScroll} on:resize={onScroll} -->
  <slot />
</div>
