<script lang="ts">
  import {
    Motion,
    useElementScroll,
    useTransform,
    useViewportScroll,
  } from "svelte-motion";

  const val = $state(useElementScroll());
  let i = val.scrollYProgress;
  let mint = $derived($i === undefined ? 1 : $i);
</script>

<div bind:this={val.ref} class="scroller">
  <div class="inner"></div>
</div>
<Motion >
  {#snippet children({ motion })}
    <div use:motion>{Math.round((100 * mint) / 1.07)}%</div>
  {/snippet}
</Motion>

<style>
  .scroller {
    position: absolute;
    overflow: scroll;
    display: inline-block;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  .inner {
    width: 500px;
    height: 900px;
  }
</style>
