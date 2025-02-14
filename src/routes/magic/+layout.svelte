<script lang="ts">
  import MagicSidebar from "$lib/magicui/components/MagicSidebar/MagicSidebar.svelte";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();

    
</script>
<MagicSidebar>
    {@render children?.()}
</MagicSidebar>