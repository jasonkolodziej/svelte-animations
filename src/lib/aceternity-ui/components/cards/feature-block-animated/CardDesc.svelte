<script lang="ts">
  import { cn } from "$lib/utils";
  interface Props {
    class?: string;
    children?: import('svelte').Snippet;
  }

  let { class: className = "", children }: Props = $props();
  
</script>

<p
  class={cn(
    "text-sm font-normal text-neutral-600 dark:text-neutral-400 max-w-sm",
    className
  )}
>
  {@render children?.()}
</p>
