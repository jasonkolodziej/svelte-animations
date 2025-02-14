<script lang="ts">
  import { spring } from "svelte/motion";
  import FollowPointer from "./FollowPointer.svelte";

  interface Props {
    title?: string;
    children?: import('svelte').Snippet;
  }

  let { title = "Coding is fun", children }: Props = $props();
  let ref = $state(null);
  let isInside = $state(false);
  let x = spring(0, { stiffness: 0.25, damping: 1.4 });
  let y = spring(0, { stiffness: 0.25, damping: 1.4 });

  const handleMouseMove = (e) => {
    if (ref) {
      let rects = ref.getBoundingClientRect();
      x.set(e.clientX - rects.left);
      y.set(e.clientY - rects.top);
    }
  };

  const handleMouseLeave = () => {
    isInside = false;
  };

  const handleMouseEnter = () => {
    isInside = true;
  };
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<div
  onmouseleave={handleMouseLeave}
  onmouseenter={handleMouseEnter}
  onmousemove={handleMouseMove}
  bind:this={ref}
  style="cursor: none"
  class="relative"
>
  {#if isInside}
    <FollowPointer x={$x} y={$y} {title} />
  {/if}
  {@render children?.()}
</div>
