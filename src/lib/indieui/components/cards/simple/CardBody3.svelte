<script lang="ts">
  import CardIcon from "./CardIcon.svelte";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();
</script>

<div>
  <div
    class="border border-dashed border-zinc-400 dark:border-zinc-700 relative"
  >
    <CardIcon class="-top-3 -left-3" />
    <CardIcon class="-top-3 -right-3" />
    <CardIcon class="-bottom-3 -left-3" />
    <CardIcon class="-bottom-3 -right-3" />
    <!-- Put Any Content inside this Slot  -->
    {@render children?.()}
  </div>
</div>
