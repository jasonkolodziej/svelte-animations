<script lang="ts">
  import { cn } from "$lib/utils";
  interface Props {
    class?: string;
    children?: import('svelte').Snippet;
  }

  let { class: className = "", children }: Props = $props();
  
</script>

<h3
  class={cn(
    "text-lg font-semibold text-gray-800 dark:text-white py-2",
    className
  )}
>
  {@render children?.()}
</h3>
