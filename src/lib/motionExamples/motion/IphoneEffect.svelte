<script>
  import { cubicInOut, expoIn, quintInOut } from "svelte/easing";
  import { crossfade } from "svelte/transition";
  let openApp = $state("");
  let apps = [
    "🐦",
    "🐱",
    "🐶",
    "🐭",
    "🐹",
    "🐰",
    "🦊",
    "🐻",
    "🐼",
    "🐨",
    "🐯",
    "🦁",
    "🐮",
    "🐷",
    "🐸",
    "🐵",
    "🐔",
    "🐧",
    "🐤",
  ];
  const [send, receive] = crossfade({
    duration: 300,
  });
</script>

<div class="flex justify-center items-center h-screen">
  <div
    class="grid grid-cols-3 place-content-center place-items-center gap-3 *:border *:border-primary *:rounded-md *:p-2 p-4 t w-full h-full md:w-48 md:h-[390px] rounded-xl md:bg-lime-100 relative"
  >
    {#each apps as app}
      {#if openApp !== app}
        <button
          class="icon transition-all duration-150 ease-in h-12 w-12 md:h-fit md:w-fit"
          onclick={() => (openApp = app)}
          in:receive={{ key: app }}
          out:send={{ key: app }}
        >
          {app}
        </button>
      {:else}
        <div
          class="app absolute bg-white w-full h-full items-center justify-center flex flex-col gap-2"
          in:receive={{ key: app }}
          out:send={{ key: app }}
        >
          <h1>Hello Devs {app}</h1>
          <button onclick={() => (openApp = "")}>Close</button>
        </div>
      {/if}
    {/each}
  </div>
</div>
