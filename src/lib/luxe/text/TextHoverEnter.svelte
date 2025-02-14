<script lang="ts">
  import { Motion } from "motion-start";

  let DURATION = 0.25;
  let STAGGER = 0.025;
  interface Props {
    text?: string;
  }

  let { text = "Hover Button" }: Props = $props();
  let letters = text
    .split("")
    .map((letter) => (letter === " " ? "\u00A0" : letter));
</script>

<Motion initial="initial" whileHover="hovered" >
  {#snippet children({ motion })}
    <div
      use:motion
      class="relative block overflow-hidden text-base font-medium text-neutral-400"
    >
      <div class="w-full px-1">
        {#each letters as letter, i}
          <Motion
            variants={{
              initial: { y: 0 },
              hovered: { y: "-100%" },
            }}
            transition={{
              duration: DURATION,
              ease: "easeInOut",
              delay: STAGGER * i,
            }}
            
          >
            {#snippet children({ motion })}
                    <span class="inline-block tracking-[-3.8px]" use:motion>{letter}</span>
                              {/snippet}
                </Motion>
        {/each}
      </div>
      <div class="absolute inset-0">
        {#each letters as letter, i}
          <Motion
            variants={{
              initial: { y: "100%" },
              hovered: { y: 0 },
            }}
            transition={{
              duration: DURATION,
              ease: "easeInOut",
              delay: STAGGER * i,
            }}
            
          >
            {#snippet children({ motion })}
                    <span class="inline-block tracking-[-3.8px]" use:motion>{letter}</span>
                              {/snippet}
                </Motion>
        {/each}
      </div>
    </div>
  {/snippet}
</Motion>
