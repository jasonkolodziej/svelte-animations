<script lang="ts">
  import { Motion} from "svelte-motion";

  interface Props {
    buttonColor?: string;
    buttonTextColor?: string;
    subscribeStatus?: boolean;
    changeText?: import('svelte').Snippet;
    initialText?: import('svelte').Snippet;
  }

  let {
    buttonColor = "#000",
    buttonTextColor = "#fff",
    subscribeStatus = false,
    changeText,
    initialText
  }: Props = $props();

  let isSubscribed = $state(subscribeStatus);
</script>

{#if isSubscribed}
  <Motion
    initial={{ opacity: 0 }}
    animate={{ opacity: 1 }}
    exit={{ opacity: 0 }}
    
  >
    {#snippet children({ motion })}
        <button
        onclick={() => (isSubscribed = !isSubscribed)}
        class="relative flex w-[200px] items-center justify-center overflow-hidden rounded-md bg-white p-[10px]"
        use:motion
      >
        <Motion initial={{ y: -50 }} animate={{ y: 0 }} >
          {#snippet children({ motion })}
                <span
              use:motion
              class="relative block h-full w-full font-semibold text-white dark:text-black"
            >
              {#if changeText}{@render changeText()}{:else}Subscribed{/if}
            </span>
                        {/snippet}
            </Motion>
      </button>
          {/snippet}
    </Motion>
{:else}
  <Motion
    initial={{ opacity: 0 }}
    animate={{ opacity: 1 }}
    exit={{ opacity: 0 }}
    
  >
    {#snippet children({ motion })}
        <button
        style=" background-color: {buttonColor}; color: {buttonTextColor};"
        onclick={() => (isSubscribed = !isSubscribed)}
        class="relative flex w-[200px] cursor-pointer items-center justify-center rounded-md border-none p-[10px]"
        use:motion
      >
        <Motion
          initial={{ x: 0 }}
          exit={{ x: 50, transition: { duration: 0.1 } }}
          
        >
          {#snippet children({ motion })}
                <span use:motion class="relative block font-semibold text-primary">
              {#if initialText}{@render initialText()}{:else}Subscribe{/if}
            </span>
                        {/snippet}
            </Motion>
      </button>
          {/snippet}
    </Motion>
{/if}
