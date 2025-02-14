<script lang="ts">
  import AceternitySidebar from "$lib/aceternity-ui/web/AceternitySidebar.svelte";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();
</script>

<AceternitySidebar>
  {@render children?.()}
</AceternitySidebar>
