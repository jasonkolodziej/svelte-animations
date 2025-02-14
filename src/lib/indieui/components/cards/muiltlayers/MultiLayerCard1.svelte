<script lang="ts">
  import MCardBody1 from "./cardbody/MCardBody1.svelte";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();
</script>

<div class="py-8">
  <div class="relative max-w-xl">
    <div
      class="absolute scale-x-95 inset-0 -rotate-[5deg] rounded-lg bg-gray-200 dark:bg-zinc-800 py-10"
></div>
    <!-- Write Content Here  -->
    {#if children}{@render children()}{:else}
      <MCardBody1
        class="px-6 py-10 relative mx-auto rounded-lg shadow dark:bg-zinc-900/90 backdrop-blur-xl"
      />
    {/if}
  </div>
</div>
