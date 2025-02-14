<script lang="ts">
  import { cn } from "$lib/utils";
  import { Motion } from "motion-start";

  
  interface Props {
    class?: any;
    r?: number;
    c?: number;
  }

  let { class: className = "", r = 5, c = 5 }: Props = $props();
  let rows = new Array(r).fill(1);
  let cols = new Array(c).fill(1);
</script>

<div class="">
  <div class={cn("relative z-0 flex w-full h-full justify-center", className)}>
    {#each rows as _, i}
      <Motion >
        {#snippet children({ motion })}
                <div
            class="md:w-12 sm:h-12 w-9 h-9 dark:border-neutral-900 border-neutral-200"
            use:motion
          >
            {#each cols as _, j}
              <Motion
                whileHover={{
                  backgroundColor: `var(--tile)`,
                  transition: { duration: 0 },
                }}
                animate={{
                  transition: { duration: 2 },
                }}
                
              >
                {#snippet children({ motion })}
                            <div
                    class="md:w-12 sm:h-12 w-9 h-9 border-r border-t last:border-b {i ===
                      0 && j >= 0
                      ? 'border-l'
                      : ''}    dark:border-neutral-900 border-neutral-200 relative"
                    use:motion
                  ></div>
                                          {/snippet}
                        </Motion>
            {/each}
          </div>
                      {/snippet}
            </Motion>
    {/each}
  </div>
</div>
