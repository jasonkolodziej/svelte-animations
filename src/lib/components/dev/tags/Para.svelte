<script lang="ts">
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();
</script>

<p class="text-primary/80  text-md mt-1.5  leading-6">
  {@render children?.()}
</p>
