<script lang="ts">
  import { slide } from "svelte/transition";
  import { vopen } from "./svelteContent";
  import { Menu, X } from "lucide-svelte";
  interface Props {
    className?: string;
    children?: import('svelte').Snippet;
  }

  let { className = "", children }: Props = $props();
</script>

<div
  class="h-10 px-4 py-4 flex flex-row md:hidden items-center justify-between bg-neutral-100 dark:bg-neutral-800 w-fit"
>
  <button
    onclick={() => {
      vopen.update((v) => !v);
      console.log("open");
    }}
    class="flex justify-end z-50 w-full"
  >
    <Menu class="text-neutral-800 dark:text-neutral-200" />
  </button>

  {#if $vopen}
    <div
      transition:slide={{ axis: "x", duration: 300 }}
      class="fixed h-full w-full inset-0 bg-white dark:bg-neutral-900 p-10 z-[400] flex flex-col justify-between {className}"
    >
      <!-- svelte-ignore a11y_no_static_element_interactions -->
      <!-- svelte-ignore a11y_click_events_have_key_events -->
      <div
        class="absolute right-10 top-10 z-50 text-neutral-800 dark:text-neutral-200"
        onclick={() => {
          vopen.update((v) => !v);
        }}
      >
        <X />
      </div>
      {@render children?.()}
    </div>
  {/if}
</div>
