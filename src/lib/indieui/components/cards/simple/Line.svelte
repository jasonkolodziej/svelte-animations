<script lang="ts">
  import { cn } from "$lib/utils";

  interface Props {
    class?: string;
  }

  let { class: className = "" }: Props = $props();
  
</script>

<div
  class={cn(
    "h-px w-full via-zinc-400 from-[1%] from-zinc-200 to-zinc-600 absolute -z-0 dark:via-zinc-700 dark:from-zinc-900 dark:to-zinc-500",
    className
  )}
></div>
