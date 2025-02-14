<script lang="ts">
  import { cn } from "$lib/utils";

  let mousePosition = $state({ x: 0, y: 0 });
  let isHovering = $state(false);
  interface Props {
    containerClass?: string;
    class?: string;
    children?: import('svelte').Snippet;
  }

  let { containerClass = "", class: _class = "", children }: Props = $props();
  

  const handleMouseMove = (event) => {
    const { clientX, clientY } = event;
    const rect = event.currentTarget.getBoundingClientRect();
    const x = (clientX - (rect.left + rect.width / 2)) / 20;
    const y = (clientY - (rect.top + rect.height / 2)) / 20;
    mousePosition = { x, y };
  };

  const handleMouseLeave = () => {
    isHovering = false;
    mousePosition = { x: 0, y: 0 };
  };
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<section
  onmousemove={handleMouseMove}
  onmouseenter={() => (isHovering = true)}
  onmouseleave={handleMouseLeave}
  style="transform: {isHovering
    ? `translate3d(${mousePosition.x}px, ${mousePosition.y}px, 0) scale3d(1, 1, 1)`
    : 'translate3d(0px, 0px, 0) scale3d(1, 1, 1)'}; transition: transform 0.1s ease-out;"
  class={cn(
    "mx-auto w-full bg-indigo-800 relative rounded-2xl overflow-hidden",
    containerClass
  )}
>
  <div
    class="relative h-full [background-image:radial-gradient(88%_100%_at_top,rgba(255,255,255,0.5),rgba(255,255,255,0))] sm:mx-0 sm:rounded-2xl overflow-hidden"
    style="box-shadow: 0 10px 32px rgba(34, 42, 53, 0.12), 0 1px 1px rgba(0, 0, 0, 0.05), 0 0 0 1px rgba(34, 42, 53, 0.05), 0 4px 6px rgba(34, 42, 53, 0.08), 0 24px 108px rgba(47, 48, 55, 0.10);"
  >
    <div
      style="transform: {isHovering
        ? `translate3d(${-mousePosition.x}px, ${-mousePosition.y}px, 0) scale3d(1.03, 1.03, 1)`
        : 'translate3d(0px, 0px, 0) scale3d(1, 1, 1)'}; transition: transform 0.1s ease-out;"
      class={cn("h-full px-4 py-20 sm:px-10", _class)}
    >
      {@render children?.()}
    </div>
  </div>
</section>
