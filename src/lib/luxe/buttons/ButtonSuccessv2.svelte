<script lang="ts">
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();
</script>

<button
  class="rounded-xl bg-gradient-to-t from-green-600 to-green-500 px-4 py-2 text-sm font-medium text-white"
>
  {#if children}{@render children()}{:else}Button{/if}
</button>
