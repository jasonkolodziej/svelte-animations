<script lang="ts">
  import { cn } from "$lib/utils";

  interface Props {
    class?: string;
    children?: import('svelte').Snippet;
  }

  let { class: _class = "", children }: Props = $props();
  
</script>

<p
  class={cn("mt-8 text-zinc-400 tracking-wide leading-relaxed text-sm", _class)}
>
  {@render children?.()}
</p>
