<script lang="ts">
  import { Motion, useMotionValue, useMotionTemplate } from "motion-start";
  import { onMount } from "svelte";
  import { cn } from "$lib/utils";

  interface Props {
    gradientSize?: number;
    gradientColor?: string;
    gradientOpacity?: number;
    class?: string;
    children?: import('svelte').Snippet;
  }

  let {
    gradientSize = 200,
    gradientColor = "#262626",
    gradientOpacity = 0.8,
    class: className = "",
    children
  }: Props = $props();
  

  let gradSize = useMotionValue(gradientSize);
  let gradColor = useMotionValue(gradientColor);
  let mouseX = useMotionValue(-gradientSize);
  let mouseY = useMotionValue(-gradientSize);

  function handleMouseMove(e: MouseEvent) {
    const rect = (e.currentTarget as HTMLDivElement).getBoundingClientRect();
    mouseX.set(e.clientX - rect.left);
    mouseY.set(e.clientY - rect.top);
  }

  function handleMouseLeave() {
    mouseX.set(-gradientSize);
    mouseY.set(-gradientSize);
  }

  onMount(() => {
    mouseX.set(-gradientSize);
    mouseY.set(-gradientSize);
  });
  let bg = useMotionTemplate`radial-gradient(${gradSize}px circle at ${mouseX}px ${mouseY}px, ${gradColor}, transparent 100%)`;
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<!-- I have added py-4 in below code, you can customize the component as per needs -->
<div
  onmousemove={handleMouseMove}
  onmouseleave={handleMouseLeave}
  class={cn(
    "group relative flex size-full overflow-hidden rounded-xl bg-neutral-100 dark:bg-neutral-900 border text-black dark:text-white justify-center py-4",
    className
  )}
>
  <div class="relative z-10">
    <!-- Default  -->
    {#if children}{@render children()}{:else}
      <div class="flex items-center justify-center h-full text-center">
        <p class="text-2xl">Magic Card</p>
      </div>
    {/if}
  </div>
  <Motion
    style={{
      background: bg,
      opacity: gradientOpacity,
    }}
    
  >
    {#snippet children({ motion })}
        <div
        use:motion
        class="pointer-events-none absolute -inset-px rounded-xl opacity-0 transition-opacity duration-300 group-hover:opacity-100"
  ></div>
          {/snippet}
    </Motion>
</div>

<style>
  .size-full {
    width: 100%;
    height: 100%;
  }
</style>
