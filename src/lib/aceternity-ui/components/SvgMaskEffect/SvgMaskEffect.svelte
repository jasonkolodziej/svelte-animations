<script lang="ts">
  import { onMount, onDestroy } from "svelte";
  import { writable } from "svelte/store";
  import maskSvg from "./mask.svg";
  import { cn } from "$lib/utils";

  interface Props {
    size?: number;
    revealSize?: number;
    class?: string;
    def?: import('svelte').Snippet;
    reveal?: import('svelte').Snippet;
  }

  let {
    size = 50,
    revealSize = 300,
    class: className = "",
    def,
    reveal
  }: Props = $props();
  

  let isHovered = $state(false);
  let mousePosition = writable({ x: 0, y: 0 });
  let containerRef = $state();

  const updateMousePosition = (e) => {
    const rect = containerRef.getBoundingClientRect();
    let x = e.clientX - rect.left;
    let y = e.clientY - rect.top;
    mousePosition.set({ x, y });
  };

  onMount(() => {
    if (containerRef) {
      containerRef.addEventListener("mousemove", updateMousePosition);
    }
  });

  onDestroy(() => {
    if (containerRef) {
      containerRef.removeEventListener("mousemove", updateMousePosition);
    }
  });

  let maskSize = $derived(isHovered ? revealSize : size);
</script>

<div bind:this={containerRef} class={cn("relative bg-white", className)}>
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <div
    class="w-full h-full flex items-center justify-center text-6xl absolute bg-black text-white bg-grid-white/[0.2]"
    style="
        mask-position: {$mousePosition.x - maskSize / 2}px {$mousePosition.y -
      maskSize / 2}px;
        mask-image: var(--mask-svg);
        mask-size: {maskSize}px;
        mask-repeat: no-repeat;
      "
  >
    <div class="absolute inset-0 bg-black h-full w-full z-0 opacity-50"></div>
    <div
      onmouseenter={() => (isHovered = true)}
      onmouseleave={() => (isHovered = false)}
      class="max-w-4xl mx-auto text-center text-white text-4xl font-bold relative z-20"
    >
      {@render def?.()}
    </div>
  </div>

  <div class="w-full h-full flex items-center justify-center text-white">
    {@render reveal?.()}
  </div>
</div>

<style>
  :root {
    --mask-svg: url("./mask.svg");
  }
</style>
