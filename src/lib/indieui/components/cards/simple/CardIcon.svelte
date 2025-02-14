<script lang="ts">
  import { cn } from "$lib/utils";

  interface Props {
    class?: string;
  }

  let { class: className = "" }: Props = $props();
  
</script>

<svg
  xmlns="http://www.w3.org/2000/svg"
  fill="none"
  viewBox="0 0 24 24"
  width={24}
  height={24}
  stroke-width="1"
  stroke="currentColor"
  class={cn("dark:text-white text-black size-6 absolute", className)}
>
  <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v12m6-6H6" />
</svg>
