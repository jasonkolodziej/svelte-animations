<script lang="ts">
  import { vopen } from "./svelteContent";
  interface Props {
    className?: string;
    children?: import('svelte').Snippet;
  }

  let { className = "", children }: Props = $props();
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<div
  style="width: {$vopen ? '200px' : '60px'}; transition: width 0.4s;"
  class="h-full px-4 py-4 hidden md:flex md:flex-col bg-neutral-100 dark:bg-neutral-800 flex-shrink-0 {className}"
  onmouseenter={() => {
    vopen.set(true);
  }}
  onmouseleave={() => {
    vopen.set(false);
  }}
>
  {@render children?.()}
</div>
