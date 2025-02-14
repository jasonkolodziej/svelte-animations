<script lang="ts">
  import { Button as ButtonPrimitive } from "bits-ui";
  import { buttonVariants, type Props, type Events } from "./index";
  import { cn } from "$lib/utils";

  type $$Props = Props;
  type $$Events = Events;

  interface Props_1 {
    class?: $$Props["class"];
    variant?: $$Props["variant"];
    size?: $$Props["size"];
    builders?: $$Props["builders"];
    children?: import('svelte').Snippet;
    [key: string]: any
  }

  let {
    class: className = undefined,
    variant = "default",
    size = "default",
    builders = [],
    children,
    ...rest
  }: Props_1 = $props();
  
</script>

<ButtonPrimitive.Root
  {builders}
  class={cn(buttonVariants({ variant, size, className }))}
  type="button"
  {...rest}
  on:click
  on:keydown
>
  {#if variant === "animated"}
    <span>
      <span
        class="spark mask-gradient animate-flip before:animate-kitrotate absolute inset-0 h-[100%] w-[100%] overflow-hidden rounded-xl [mask:linear-gradient(white,_transparent_50%)] before:absolute before:aspect-square before:w-[200%] before:rotate-[-90deg] before:bg-[conic-gradient(from_0deg,transparent_0_340deg,white_360deg)] before:content-[''] before:[inset:0_auto_auto_50%] before:[translate:-50%_-15%]"
></span>
    </span>
    <span
      class="backdrop absolute inset-px rounded-[11px] bg-neutral-950 transition-colors duration-200 group-hover:bg-neutral-900"
></span>
    <span class="z-10 text-neutral-400 text-sm font-medium">
      {#if children}{@render children()}{:else}Button{/if}
    </span>
  {:else}
    {@render children?.()}
  {/if}
</ButtonPrimitive.Root>
