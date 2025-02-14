<script lang="ts">
  interface Props {
    minHeight?: number;
    cls?: string;
    children?: import('svelte').Snippet;
  }

  let { minHeight = 350, cls = "", children }: Props = $props();
</script>

<div
  style="min-height: {minHeight}px; height:fit-content; touch-action: none;"
  class="{cls} dark:bg-white/5 flex justify-center items-center border border-primary/40 rounded-xl my-2 p-4 md:p-6 w-full"
>
  {@render children?.()}
</div>
