<script lang="ts">
  import MainSidebar from "$lib/components/dev/tags/MainSidebar.svelte";
  import SideNav from "$lib/components/dev/tags/SideNav.svelte";
  import { animationExamples } from "$lib/examples/AnimationsExamples";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();
</script>

<MainSidebar>
  {@render children?.()}
</MainSidebar>

<!-- <SideNav examplesList={animationExamples}>
  <slot></slot>
</SideNav> -->
