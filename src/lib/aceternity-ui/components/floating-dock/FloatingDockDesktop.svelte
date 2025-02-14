<script lang="ts">
  import { Motion, useMotionValue } from "motion-start";
  import IconContainer from "./IconContainer.svelte";

  type Item = {
    title: string;
    icon: any;
    href: string;
  };
  interface Props {
    items?: Item[];
    className?: string;
  }

  let { items = [], className = "" }: Props = $props();

  const mouseX = useMotionValue(Infinity);
  const containerX = useMotionValue(0);

  let containerRef: HTMLDivElement = $state();
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<Motion >
  {#snippet children({ motion })}
    <div
      use:motion
      bind:this={containerRef}
      onmouseleave={() => mouseX.set(Infinity)}
      onmousemove={(e) => {
        const rect = containerRef.getBoundingClientRect();
        if (rect) {
          mouseX.set(e.clientX - rect.left);
          containerX.set(rect.x);
        }
      }}
      class="mx-auto hidden md:flex h-16 gap-4 items-end rounded-2xl bg-gray-50 dark:bg-neutral-900 px-4 pb-3 {className}"
    >
      {#each items as item (item.title)}
        <IconContainer {mouseX} {containerX} {...item} />
      {/each}
    </div>
  {/snippet}
</Motion>
