<script lang="ts">
  import { cn } from "$lib/utils";
  import { AnimatePresence, Motion } from "svelte-motion";

  

  interface Props {
    class?: any;
    words?: string;
    delay?: number;
    variants?: any;
  }

  let {
    class: className = "",
    words = "Fade In",
    delay = 0.19,
    variants = {
    hidden: { opacity: 0 },
    visible: (i: any) => ({
      y: 0,
      opacity: 1,
      transition: { delay: i * delay },
    }),
  }
  }: Props = $props();
  let wordsspilit = words.split(" ");
</script>

<Motion {variants} initial="hidden" animate="visible" >
  {#snippet children({ motion })}
    <h1
      class={cn(
        "font-display text-center text-4xl font-bold tracking-[-0.02em] text-black drop-shadow-sm dark:text-white md:text-7xl md:leading-[5rem]",
        className
      )}
      use:motion
    >
      {#each wordsspilit as word, i}
        <Motion {variants} custom={i} >
          {#snippet children({ motion })}
                <span use:motion> {word}</span>
                        {/snippet}
            </Motion>
      {/each}
    </h1>
  {/snippet}
</Motion>
