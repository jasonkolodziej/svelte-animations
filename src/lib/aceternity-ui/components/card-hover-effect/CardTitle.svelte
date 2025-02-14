<script lang="ts">
  import { cn } from "$lib/utils";

  interface Props {
    class?: string;
    children?: import('svelte').Snippet;
  }

  let { class: _class = "", children }: Props = $props();
  
</script>

<h4 class={cn("text-zinc-100 font-bold tracking-wide mt-4", _class)}>
  {@render children?.()}
</h4>
