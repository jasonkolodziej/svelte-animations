<script lang="ts">
  import { run } from 'svelte/legacy';

  import { cn } from "$lib/utils";
  import { getContext } from "svelte";
  import { Motion, useSpring, useTransform } from "motion-start";

  let DEFAULT_MAGNIFICATION = 60;
  let DEFAULT_DISTANCE = 140;
  
  let mouseX = getContext("mouseX");
  run(() => {
    console.log(mouseX.current, "---");
  });
  interface Props {
    class?: string;
    distance?: number;
    magnification?: number;
    children?: import('svelte').Snippet;
  }

  let {
    class: className = "",
    distance = DEFAULT_DISTANCE,
    magnification = DEFAULT_MAGNIFICATION,
    children
  }: Props = $props();
  let ref: HTMLElement = $state();
  let distanceCalc = useTransform(mouseX, (val: number) => {
    const bounds = ref?.getBoundingClientRect() ?? { x: 0, width: 0 };

    return val - bounds.x - bounds.width / 2;
  });
  let widthSync = useTransform(
    distanceCalc,
    [-distance, 0, distance],
    [40, magnification, 40]
  );
  let width = useSpring(widthSync, { stiffness: 150, damping: 12, mass: 0.1 });

  const children_render = $derived(children);
</script>

<Motion style={{ width }} >
  {#snippet children({ motion })}
    <div
      class={cn(
        "flex aspect-square cursor-pointer items-center justify-center rounded-full",
        className
      )}
      bind:this={ref}
      use:motion
    >
      {#if children_render}{@render children_render()}{:else}
        <!-- Default -->DockIcon
      {/if}
    </div>
  {/snippet}
</Motion>
