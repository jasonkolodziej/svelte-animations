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
    "rounded-2xl h-full w-full p-4 overflow-hidden bg-black border border-transparent dark:border-white/[0.2] group-hover:border-slate-700 relative z-20",
    _class
  )}
>
  <div class="relative z-50">
    <div class="p-4">
      {@render children?.()}
    </div>
  </div>
</div>
