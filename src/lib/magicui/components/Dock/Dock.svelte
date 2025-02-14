<script lang="ts">
  import { cn } from "$lib/utils";
  import { setContext } from "svelte";
  import { Motion, useMotionValue } from "svelte-motion";
  let DEFAULT_MAGNIFICATION = 60;
  let DEFAULT_DISTANCE = 140;
  interface Props {
    direction?: "top" | "middle" | "bottom";
    distance?: number;
    magnification?: number;
    children?: import('svelte').Snippet<[any]>;
  }

  let {
    direction = "top",
    distance = DEFAULT_DISTANCE,
    magnification = DEFAULT_MAGNIFICATION,
    children
  }: Props = $props();

  let dockVariants = cn(
    "mx-auto w-max mt-8 h-[58px] p-2 flex gap-2 rounded-2xl border supports-backdrop-blur:bg-white/10 supports-backdrop-blur:dark:bg-black/10 backdrop-blur-md"
  );
  let mouseX = useMotionValue(Infinity);
  setContext("mouseX", mouseX);

  const children_render = $derived(children);
</script>

<Motion >
  {#snippet children({ motion })}
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div
      onmousemove={(e) => mouseX.set(e.pageX)}
      onmouseleave={() => mouseX.set(Infinity)}
      use:motion
      class={cn(dockVariants, {
        "items-start": direction === "top",
        "items-center": direction === "middle",
        "items-end": direction === "bottom",
      })}
    >
      {#if children_render}{@render children_render({ mouseX, })}{:else}
        <!-- Default -->Dock
      {/if}
    </div>
  {/snippet}
</Motion>
