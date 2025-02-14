<script lang="ts">
  import LuxeSidebar from "$lib/luxe/components/sidebar/LuxeSidebar.svelte";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();

</script>


<LuxeSidebar>
    {@render children?.()}
</LuxeSidebar>