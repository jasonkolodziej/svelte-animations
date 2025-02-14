<script lang="ts">
  

  import { cn } from "$lib/utils";
  import { Motion } from "motion-start";
  interface Props {
    class?: string;
    children?: import('svelte').Snippet;
  }

  let { class: _class = "", children }: Props = $props();

  let position = $state({ x: 0, y: 0 });
  let ref: HTMLButtonElement | null = $state(null);

  let handleMouseMove = (e: MouseEvent) => {
    let { clientX, clientY } = e;
    let { height, width, left, top } = ref.getBoundingClientRect();

    let middleX = clientX - (left + width / 2);
    let middleY = clientY - (top + height / 2);

    position.x = middleX;
    position.y = middleY;
  };

  let handleMouseLeave = () => {
    position.x = 0;
    position.y = 0;
  };

  const children_render = $derived(children);
</script>

<Motion
  
  animate={{ x: position.x, y: position.y }}
  transition={{
    type: "spring",
    damping: 15,
    stiffness: 150,
    mass: 0.1,
  }}
>
  {#snippet children({ motion })}
    <button
      class={cn(
        "relative rounded-xl bg-white px-4 py-2 text-sm font-semibold text-black",
        _class
      )}
      bind:this={ref}
      onmousemove={handleMouseMove}
      onmouseleave={handleMouseLeave}
      use:motion
    >
      {#if children_render}{@render children_render()}{:else}Button{/if}
    </button>
  {/snippet}
</Motion>
