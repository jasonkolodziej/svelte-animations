<script>
  import { Motion, AnimateSharedLayout } from "svelte-motion";
  const tabs = [
    {
      title: "All Posts",
    },
    {
      title: "Interactions",
    },
    {
      title: "Resources",
    },
    {
      title: "Docs",
    },
  ];
  let activeIdx = $state(0);
</script>

<div class="relative flex flex-wrap items-center justify-center">
  <AnimateSharedLayout>
    {#each tabs as item, i}
      <button
        class="group relative z-[1] rounded-full px-3 py-2 {activeIdx === i
          ? 'z-0'
          : ''} "
        onclick={() => {
          activeIdx = i;
        }}
      >
        {#if activeIdx === i}
          <Motion
            layoutId="clicked-btn"
            transition={{ duration: 0.2, type:'spring', stiffness: 300, damping: 30 }}
            
          >
            {#snippet children({ motion })}
                        <div
                use:motion
                class="absolute inset-0 rounded-full bg-white"
              ></div>
                                  {/snippet}
                    </Motion>
        {/if}
        <span
          class="relative text-sm block font-medium duration-200 {activeIdx ===
          i
            ? 'text-black delay-100'
            : 'text-white'}"
        >
          {item.title}
        </span>
      </button>
    {/each}
  </AnimateSharedLayout>
</div>
