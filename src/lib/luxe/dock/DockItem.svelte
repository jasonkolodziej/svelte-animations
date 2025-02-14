<script lang="ts">
  import { useSpring, useTransform, Motion } from "svelte-motion";
  import type { MotionValue } from "svelte-motion";

  interface Props {
    containerX: MotionValue<number>;
    mouseX: MotionValue<number>;
    children?: import('svelte').Snippet;
  }

  let { containerX, mouseX, children }: Props = $props();

  let dockItem: HTMLDivElement = $state();

  let distance = useTransform(mouseX, (val) => {
    const bounds = dockItem?.getBoundingClientRect() ?? {
      x: 0,
      width: 0,
      left: 0,
    };

    const XDiffToContainerX = bounds?.x - containerX.get();

    return val - bounds?.width / 2 - XDiffToContainerX;
  });
  let widthSync = useTransform(distance, [-125, 0, 125], [44, 85, 44]);
  //   Adjust stiffness and damping as per needs 
  let width = useSpring(widthSync, { stiffness: 400, damping: 25 });

  const children_render = $derived(children);
</script>

<Motion
  
  style={{ width: width }}
  transition={{
    bounceDamping: 300,
    bounceStiffness: 800,
    bounce: 0.3,
    duration: 0.8,
  }}
>
  {#snippet children({ motion })}
    <div
      role="button"
      bind:this={dockItem}
      use:motion
      class="group p-2 flex aspect-square items-center justify-center overflow-hidden rounded-full transition active:-translate-y-10 bg-neutral-950 border-neutral-800 border shadow-inner shadow-neutral-300/20 active:duration-1000 active:ease-out text-neutral-400 hover:text-white duration-500"
    >
      {@render children_render?.()}
    </div>
  {/snippet}
</Motion>
