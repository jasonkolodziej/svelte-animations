<script>
  import Box from "$lib/components/dev/tags/Box.svelte";
  import { Motion, useAnimation } from "svelte-motion";
  let controls = useAnimation();
</script>

<Box cls="bg-slate-800 text-black" minHeight={450}>
  <div
    class="bg-gray-500/10 h-80  w-80 flex justify-center items-center rounded-xl shadow-md"
  >
    <Motion
      
      drag={true}
      dragConstraints={{
        top: -100,
        bottom: 100,
        right: 100,
        left: -100,
      }}
      dragTransition={{
        bounceStiffness: 600,
        bounceDamping: 20,
      }}
      
      dragElastic={0.5}
      whileTap={{
        cursor: "grabbing",
      }}
      
      >{#snippet children({ motion })}
            <div class="box" use:motion>Smooth Drag</div>          {/snippet}
        </Motion
    >
  </div>
</Box>
