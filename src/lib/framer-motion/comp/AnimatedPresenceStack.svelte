<script>
  import { run } from 'svelte/legacy';

  import { Motion, AnimatePresence } from "svelte-motion";
  import Card from "./Card.svelte";
  let index = $state(0);
  let mint;
  run(() => {
    mint = index + 1;
  });
</script>

<Motion >
  {#snippet children({ motion })}
    <div
      use:motion
      class="w-64 h-64 relative bg-gray-700/40 rounded-lg flex justify-center items-center"
    >
      <AnimatePresence initial={false}  list={[{ key: index }]}>
        {#snippet children({ item })}
            <Card bind:index={mint} frontCard={false} />
          <Card bind:index drag="x" frontCard={true} />
                  {/snippet}
        </AnimatePresence>
    </div>
  {/snippet}
</Motion>
