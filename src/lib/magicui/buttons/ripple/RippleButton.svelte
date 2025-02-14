<script lang="ts">
  import { cn } from "$lib/utils";
  
  interface Props {
    class?: string;
    duration?: string;
    rippleColor?: string;
    children?: import('svelte').Snippet;
    [key: string]: any
  }

  let {
    class: _class = "",
    duration = "2000ms",
    rippleColor = "#fff",
    children,
    ...rest
  }: Props = $props();

  let buttonRipples: Array<{
    x: number;
    y: number;
    size: number;
    key: number;
  }> = $state([]);

  let createRipple = (event: MouseEvent) => {
    const button = event.currentTarget as HTMLButtonElement;
    const rect = button.getBoundingClientRect();
    const size = Math.max(rect.width, rect.height);
    const x = event.clientX - rect.left - size / 2;
    const y = event.clientY - rect.top - size / 2;

    let newRipple = { x, y, size, key: Date.now() };

    buttonRipples = [...buttonRipples, newRipple];

    // Remove the ripple after 2 seconds
    // This is to prevent memory leaks
    setTimeout(() => {
      buttonRipples = buttonRipples.filter(
        (ripple) => ripple.key !== newRipple.key
      );
    }, parseInt(duration));
  };
</script>

<button
  onclick={createRipple}
  {...rest}
  class={cn(
    "relative flex cursor-pointer items-center justify-center overflow-hidden rounded-lg border-2 bg-background px-4 py-2 text-center text-primary",
    _class
  )}
>
  <div class="relative z-10">
    {#if children}{@render children()}{:else}Ripple{/if}
  </div>
  <span class="pointer-events-none absolute inset-0">
    {#each buttonRipples as ripple}
      <span
        class="absolute animate-rippling rounded-full bg-background opacity-30"
        style="
          width: {ripple.size}px;
          height: {ripple.size}px;
          top: {ripple.y}px;
          left: {ripple.x}px;
          background-color: {rippleColor};
          transform : scale(0);
        "
></span>
    {/each}
  </span>
</button>
