<script lang="ts">
  import { cn } from "$lib/utils";

  interface Props {
    class?: string;
    children?: import('svelte').Snippet;
  }

  let { class: _class = "", children }: Props = $props();
  
</script>

<div
  class={cn(
    "grid md:auto-rows-[18rem] grid-cols-1 md:grid-cols-3 gap-4 max-w-7xl mx-auto ",
    _class
  )}
>
  {@render children?.()}
</div>
