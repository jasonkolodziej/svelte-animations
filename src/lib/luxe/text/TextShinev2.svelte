<script lang="ts">
  import { Motion } from "motion-start";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();

  const children_render = $derived(children);
</script>

<Motion
  
  initial={{ backgroundPosition: "200% 0" }}
  animate={{ backgroundPosition: "-200% 0" }}
  transition={{
    repeat: Infinity,
    duration: 2,
    ease: "linear",
  }}
>
  {#snippet children({ motion })}
    <h1
      use:motion
      class="bg-[linear-gradient(110deg,#404040,35%,#fff,50%,#404040,75%,#404040)] bg-[length:200%_100%] bg-clip-text text-base font-medium text-transparent"
    >
      {#if children_render}{@render children_render()}{:else}Generating Code..{/if}
    </h1>
  {/snippet}
</Motion>
