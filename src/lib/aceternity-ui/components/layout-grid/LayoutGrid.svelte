<script lang="ts">
  import { cn } from "$lib/utils";
  import type { ComponentType } from "svelte";
  import { Motion, AnimatePresence, AnimateSharedLayout } from "svelte-motion";

  type Card = {
    id: number;
    content: string | ComponentType;
    class: string;
    thumbnail: string;
  };
  let selected: Card | null = $state(null);
  let lastSelected: Card | null = $state(null);

  let handleClick = (card: Card) => {
    lastSelected = selected;
    selected = card;
  };

  let handleOutsideClick = () => {
    lastSelected = selected;
    selected = null;
  };
  interface Props {
    cards?: Card[];
  }

  let { cards = [] }: Props = $props();
</script>

<div
  class="w-full h-full p-10 grid grid-cols-1 md:grid-cols-3 max-w-7xl mx-auto gap-4 relative"
>
  <AnimateSharedLayout type='crossfade'>
    {#each cards as card, i}
      <div class={cn(card.class)}>
        <Motion layoutId={`card-${card.id}`} >
          {#snippet children({ motion })}
                    <!-- svelte-ignore a11y_click_events_have_key_events -->
            <!-- svelte-ignore a11y_no_static_element_interactions -->
            <div
              onclick={() => {
                handleClick(card);
              }}
              class={cn(
                card.class,
                "relative overflow-hidden",
                selected?.id === card.id
                  ? "rounded-lg cursor-pointer absolute inset-0 h-1/2 w-full md:w-1/2 m-auto z-50 flex justify-center items-center flex-wrap flex-col"
                  : lastSelected?.id === card.id
                    ? "z-40 bg-white rounded-xl h-full w-full"
                    : "bg-white rounded-xl h-full w-full"
              )}
              use:motion
            >
              <!-- Need to Update below comp -->
              {#if selected?.id === card.id}
                <div
                  class="bg-transparent h-full w-full flex flex-col justify-end rounded-lg shadow-2xl relative z-[60]"
                >
                  <Motion
                    initial={{
                      opacity: 0,
                    }}
                    animate={{
                      opacity: 0.6,
                    }}
                    
                  >
                    {#snippet children({ motion })}
                                    <div
                        use:motion
                        class="absolute inset-0 h-full w-full  bg-black opacity-100 z-10"
                      >
                        <Motion
                          layoutId={`content-${selected?.id}`}
                          initial={{
                            opacity: 0,
                            y: 100,
                          }}
                          animate={{
                            opacity: 1,
                            y: 0,
                          }}
                          exit={{
                            opacity: 0,
                            y: 100,
                          }}
                          transition={{
                            duration: 0.3,
                            ease: "easeInOut",
                          }}
                          
                        >
                          {#snippet children({ motion })}
                                            <div use:motion class="relative px-8 pb-4 z-[70] top-8 md:top-36">
                              {#if typeof selected?.content === "string"}
                                <p class="text-white text-2xl mt-3 font-bold ">
                                  {selected?.content}
                                </p>
                              {:else}
                                {@const SvelteComponent = selected?.content}
                          <SvelteComponent />
                              {/if}
                            </div>
                                                                    {/snippet}
                                        </Motion>
                      </div>
                                                      {/snippet}
                                </Motion>
                </div>
                <!-- {:else} -->
              {/if}
              <Motion layoutId={`image-${card.id}-image`} >
                {#snippet children({ motion })}
                            <img
                    use:motion
                    src={card.thumbnail}
                    alt="thumbnail"
                    height="500"
                    width="500"
                    class={cn(
                      "object-cover object-top absolute inset-0 h-full w-full transition duration-200"
                    )}
                  />
                                          {/snippet}
                        </Motion>
            </div>
                            {/snippet}
                </Motion>
      </div>
    {/each}
  </AnimateSharedLayout>
  <Motion animate={{ opacity: selected?.id ? 0.3 : 0 }} >
    {#snippet children({ motion })}
        <!-- svelte-ignore a11y_click_events_have_key_events -->
      <!-- svelte-ignore a11y_no_static_element_interactions -->
      <div
        use:motion
        onclick={handleOutsideClick}
        class={cn(
          "absolute h-full w-full left-0 top-0 bg-black opacity-0 z-10",
          selected?.id ? "pointer-events-auto" : "pointer-events-none"
        )}
      ></div>
          {/snippet}
    </Motion>
</div>
