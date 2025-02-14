<script lang="ts">
  import { cubicOut } from "svelte/easing";
  import { onMount } from "svelte";
  import { spring, tweened } from "svelte/motion";
  import { cn } from "$lib/utils";
  let num = tweened(initial, {
    duration: duration,
    easing: cubicOut,
  });
  interface Props {
    value?: number;
    initial?: number;
    duration?: number;
    class?: any;
    [key: string]: any
  }

  let {
    value = 100,
    initial = 0,
    duration = 6000,
    class: className = "",
    ...rest
  }: Props = $props();
  
  onMount(() => {
    num.set(value);
  });
</script>

<div
  class={cn(
    "inline-block  text-black dark:text-white tracking-normal",
    className
  )}
  {...rest}
>
  {$num.toFixed(0)}
</div>
