<script lang="ts">
  import { cn } from "$lib/utils";
  import DesktopSidebar from "./DesktopSidebar.svelte";
  import MobileSidebar from "./MobileSidebar.svelte";
  interface Props {
    class?: string;
    children?: import('svelte').Snippet;
  }

  let { class: _class = "", children }: Props = $props();
  
</script>

<div class={cn(_class)}>
  <DesktopSidebar>
    {@render children?.()}
  </DesktopSidebar>
  <MobileSidebar>
    {@render children?.()}
  </MobileSidebar>
</div>
