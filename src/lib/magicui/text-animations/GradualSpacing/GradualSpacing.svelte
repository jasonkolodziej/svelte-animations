<script lang="ts">
  import { cn } from "$lib/utils";
  import { AnimatePresence, Motion } from "svelte-motion";

  

  interface Props {
    class?: any;
    words?: string;
    duration?: number;
    delayMultiple?: number;
    framerProps?: any;
  }

  let {
    class: className = "Gradual Spacing",
    words = "Gradual Spacing",
    duration = 0.5,
    delayMultiple = 0.04,
    framerProps = {
    hidden: { opacity: 0, x: -20 },
    visible: { opacity: 1, x: 0 },
  }
  }: Props = $props();
  let wordsspilit = words.split("");
</script>

<div class="flex justify-center space-x-1">
  <AnimatePresence  list={[{ key: wordsspilit }]}>
    {#snippet children({ item })}
        {#each wordsspilit as char, i}
        <Motion
          initial="hidden"
          animate="visible"
          exit="hidden"
          variants={framerProps}
          transition={{
            duration: duration,
            delay: i * delayMultiple,
          }}
          
        >
          {#snippet children({ motion })}
                <span use:motion class={cn("drop-shadow-sm", className)}>
              {#if char === " "}
                <span>&nbsp;</span>
              {:else}
                {char}
              {/if}
            </span>
                        {/snippet}
            </Motion>
      {/each}
          {/snippet}
    </AnimatePresence>
</div>
