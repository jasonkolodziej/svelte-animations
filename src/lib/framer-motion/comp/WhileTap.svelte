<script lang="ts">
  import Box from "$lib/components/dev/tags/Box.svelte";
  import { Motion } from "motion-start";
</script>

<Box cls="bg-slate-800 flex gap-3 md:gap-10 text-black">
  <Motion
    whileTap={{
      rotate: 45,
      scale: 0.75,
    }}
    >{#snippet children({ motion })}
        <div class="box" use:motion>Rotate</div>      {/snippet}
    </Motion
  >
  <Motion
    whileTap={{
      scale: 0.84,
    }}
    >{#snippet children({ motion })}
        <div class="box" use:motion>Simple</div>      {/snippet}
    </Motion
  >
</Box>
