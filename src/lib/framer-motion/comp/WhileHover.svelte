<script>
  import Box from "$lib/components/dev/tags/Box.svelte";
    import { Motion } from "svelte-motion";
  </script>
  
  <Box cls="bg-slate-800 flex gap-3 md:gap-10 flex-col md:flex-row text-black">
      <Motion
        whileHover={{
          scale: 0.86,
        }}
        >{#snippet children({ motion })}
        <div class="box" use:motion>
            Scale
          </div>      {/snippet}
    </Motion
      >
      <Motion
        whileHover={{
          scale: 0.8,
          rotate: 45,
        }}
        >{#snippet children({ motion })}
        <div class="box" use:motion>
            Hover Rotate
          </div>      {/snippet}
    </Motion
      >
      <Motion
        whileHover={{
          backgroundColor: "#0091FF",
        }}
        >{#snippet children({ motion })}
        <div class="box" use:motion>
            BgColor
          </div>      {/snippet}
    </Motion
      >
  </Box>
  