<script lang="ts">
  import { cn } from "$lib/utils";

  interface Props {
    class?: any;
  }

  let { class: className = "p-4" }: Props = $props();
  
  let cardContent = {
    title: "Svelte is Vibe",
    description:
      "Svelte is a fun way to build web applications.",
  };
</script>

<div class={cn("text-left", className)}>
  <h3 class="text-lg font-bold mb-1 text-gray-900 dark:text-gray-100">
    {cardContent.title}
  </h3>
  <p class="text-gray-700 dark:text-gray-300">
    {cardContent.description}
  </p>

</div>
