<script lang="ts">
  import IndieUIsidebar from "$lib/indieui/ui/sidebar/IndieUIsidebar.svelte";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();
</script>

<IndieUIsidebar>
  {@render children?.()}
</IndieUIsidebar>
