<script lang="ts">
  interface Props {
    href?: string;
    children?: import('svelte').Snippet;
  }

  let { href = "", children }: Props = $props();
</script>

<button
  class="group relative grid overflow-hidden rounded-xl px-4 py-2 shadow-[0_1000px_0_0_hsl(0_0%_20%)_inset] transition-colors duration-200"
>
  <span>
    <span
      class="spark mask-gradient animate-flip before:animate-kitrotate absolute inset-0 h-[100%] w-[100%] overflow-hidden rounded-xl [mask:linear-gradient(white,_transparent_50%)] before:absolute before:aspect-square before:w-[200%] before:rotate-[-90deg] before:bg-[conic-gradient(from_0deg,transparent_0_340deg,white_360deg)] before:content-[''] before:[inset:0_auto_auto_50%] before:[translate:-50%_-15%]"
></span>
  </span>
  <span
    class="backdrop absolute inset-px rounded-[11px] bg-neutral-950 transition-colors duration-200 group-hover:bg-neutral-900"
></span>
  {#if href.length > 0}
    <a {href} class="z-10 text-neutral-400 text-sm font-medium">
      {#if children}{@render children()}{:else}Button{/if}
    </a>
  {:else}
    <span class="z-10 text-neutral-400 text-sm font-medium">
      {#if children}{@render children()}{:else}Button{/if}
    </span>
  {/if}
</button>
