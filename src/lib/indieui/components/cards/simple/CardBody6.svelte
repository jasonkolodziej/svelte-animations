<script lang="ts">
  import { cn } from "$lib/utils";

  let card = {
    title: "3D Card",
    desc: "Don't take above two words seriously, I just made them up.",
  };
  interface Props {
    class?: string;
  }

  let { class: className = "p-8" }: Props = $props();
  
</script>

<div class={cn("text-left", className)}>
  <h3 class="text-lg mb-1 font-bold text-gray-900 dark:text-gray-100">
    {card.title}
  </h3>
  <p class="text-gray-700 dark:text-gray-300">
    {card.desc}
  </p>
</div>
