<script lang="ts">
  import { cn } from "$lib/utils";
  import { Motion, AnimateSharedLayout, AnimatePresence } from "svelte-motion";
  import Card from "./Card.svelte";
  import CardTitle from "./CardTitle.svelte";
  import CardDesc from "./CardDesc.svelte";
  
  type Item = {
    title: string;
    desc: string;
    link: string;
  };
  interface Props {
    class?: string;
    items?: Item[];
  }

  let { class: _class = "", items = [] }: Props = $props();
  let hoveredIndex: number | null = $state(null);
</script>

<div
  class={cn("grid grid-cols-1 md:grid-cols-2  lg:grid-cols-3  py-10", _class)}
>
  <AnimateSharedLayout>
    {#each items as item, idx}
      <a
        class="relative group block p-2 h-full w-full"
        onmouseenter={() => (hoveredIndex = idx)}
        href={item.link}
      >
        {#if hoveredIndex === idx}
          <Motion
            layoutId="hoverBackground"
            initial={{ opacity: 0 }}
            animate={{
              opacity: 1,
              transition: { duration: 0.15 },
            }}
            exit={{
              opacity: 0,
              transition: { duration: 0.15, delay: 0.2 },
            }}
            
          >
            {#snippet children({ motion })}
                        <span
                use:motion
                class="absolute inset-0 h-full w-full bg-neutral-200 dark:bg-slate-800/[0.8] block rounded-3xl"
              >
              </span>
                                  {/snippet}
                    </Motion>
        {/if}
        <Card>
          <CardTitle>
            {item.title}
          </CardTitle>
          <CardDesc>
            {item.desc}
          </CardDesc>
        </Card>
      </a>
    {/each}
  </AnimateSharedLayout>
</div>
