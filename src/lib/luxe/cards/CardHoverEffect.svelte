<script lang="ts">
  import { Motion, AnimateSharedLayout, AnimatePresence } from "svelte-motion";
  import { cn } from "$lib/utils";

  let hoverdIdx = $state(0);
  const items = [
    {
      id: 1,
      title: "Framer Motion ",
      description:
        "Explore the new website that simplifies the creation of sophisticated dark mode components.",
      href: "https://animation-svelte.vercel.app/learnings",
    },
    {
      id: 2,
      title: "Svelte Animations",
      description:
        "Explore the new website that simplifies the creation of sophisticated dark mode components.",
      href: "https://animation-svelte.vercel.app",
    },
    {
      id: 3,
      title: "Github",
      description:
        "Explore the new website that simplifies the creation of sophisticated dark mode components.",
      href: "https://github.com/SikandarJODD/svelte-animations",
    },
  ];
  interface Props {
    containerClassName?: string;
  }

  let { containerClassName = "" }: Props = $props();
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<div
  onmouseleave={() => {
    hoverdIdx = 0;
  }}
  class={cn("grid md:grid-cols-3 ", containerClassName)}
>
  <AnimateSharedLayout>
    {#each items as one, i}
      <a
        href={one.href}
        target="_blank"
        onmouseenter={() => (hoverdIdx = one.id)}
        class="relative flex flex-col gap-3 p-4"
      >
        {#if hoverdIdx === one.id}
          <AnimatePresence  list={[{ key: hoverdIdx }]}>
            {#snippet children({ item })}
                        <Motion
                layoutId="cardeffect"
                initial={{ opacity: 0 }}
                animate={{
                  opacity: 1,
                  transition: { duration: 0.15 },
                }}
                exit={{
                  opacity: 0.8,
                  transition: { duration: 2, delay: 0.2 },
                }}
                
              >
                {#snippet children({ motion })}
                            <span
                    use:motion
                    class="absolute inset-0 z-0 block h-full w-full rounded-xl bg-neutral-900 cardHoverEffect"
                  >
                  </span>
                                          {/snippet}
                        </Motion>
                                  {/snippet}
                    </AnimatePresence>
        {/if}
        <div class="z-[1] space-y-3">
          <h1 class="font-medium text-white {hoverdIdx === i + 1 ? 'text-orange-400 transition-all duration-300':'' }">
            {one.title}
          </h1>
          <p class="text-neutral-400">{one.description}</p>
        </div>
      </a>
    {/each}
  </AnimateSharedLayout>
</div>
