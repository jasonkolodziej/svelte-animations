<script lang="ts">
  import { Motion, useTransform } from "motion-start";
  interface Props {
    progress?: any;
    range: [number, number];
    wordsLen?: number;
    children?: import('svelte').Snippet;
  }

  let {
    progress = 0,
    range,
    wordsLen = 0,
    children
  }: Props = $props();
  let rangeValue1 = range[0] / wordsLen;
  let rangeValue2 = range[1] / wordsLen;
  let opacity = useTransform(progress, [rangeValue1, rangeValue2], [0.2, 1]);

  const children_render = $derived(children);
</script>

<span class="xl:lg-3 relative mx-1 lg:mx-2.5">
  <span class="absolute opacity-30">
    {@render children?.()}
  </span>
  <Motion style={{ opacity: opacity }} >
    {#snippet children({ motion })}
        <span class="text-black dark:text-white" use:motion>
        {@render children_render?.()}
      </span>
          {/snippet}
    </Motion>
</span>
