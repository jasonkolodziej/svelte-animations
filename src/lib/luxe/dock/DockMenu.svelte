<script lang="ts">
  import { Motion, useMotionValue } from "motion-start";
  import { cn } from "$lib/utils";
  import DockItem from "./DockItem.svelte";
  import { AlbumIcon, HomeIcon, MonitorIcon } from "lucide-svelte";

  type DockItemProps = {
    id: string;
    icon?: {
      component: any;
      props?: Record<string, any>;
    };
  };

  const icons: Record<string, DockItemProps["icon"]> = {
    homeIcon: {
      component: HomeIcon,
      props: {
        size: 32,
      },
    },
    albumIcon: {
      component: AlbumIcon,
      props: {
        size: 32,
      },
    },
    monitorIcon: {
      component: MonitorIcon,
      props: {
        size: 32,
      },
    },
  };

  interface Props {
    side?: "top" | "bottom";
    class: string;
    [key: string]: any
  }

  let { side = "bottom", class: className, ...rest }: Props = $props();
  
  export const items: DockItemProps[] = [
    { id: "1", icon: icons["homeIcon"] },
    { id: "2", icon: icons["albumIcon"] },
    { id: "3", icon: icons["monitorIcon"] },
  ];

  const mouseX = useMotionValue(Infinity);
  const containerX = useMotionValue(0);

  let containerRef: HTMLDivElement = $state();
</script>

<div
  class={cn(side === "top" ? "top-4" : "bottom-4", className)}
  {...rest}
>
  <Motion.div 
  >
    <!-- {#snippet children({ motion })} -->
        <!-- svelte-ignore a11y_no_static_element_interactions -->
      <!-- <div
        use:motion
        bind:this={containerRef}
        class="h-16 items-end gap-4 rounded-full bg-neutral-950 border border-neutral-800 px-3 pb-2 flex shadow-inner shadow-neutral-300/5"
        onmouseleave={() => mouseX.set(Infinity)}
        onmousemove={(e) => {
          const rect = containerRef.getBoundingClientRect();
          if (rect) {
            mouseX.set(e.clientX - rect.left);
            containerX.set(rect.x);
          }
        }}
      > -->
      <div
      bind:this={containerRef}
      class="h-16 items-end gap-4 rounded-full bg-neutral-950 border border-neutral-800 px-3 pb-2 flex shadow-inner shadow-neutral-300/5"
      onmouseleave={() => mouseX.set(Infinity)}
      onmousemove={(e) => {
        const rect = containerRef.getBoundingClientRect();
        if (rect) {
          mouseX.set(e.clientX - rect.left);
          containerX.set(rect.x);
        }
      }}
    >
        {#each items as dockItem}
        
          <DockItem {containerX} {mouseX}>
            {#if dockItem?.icon}
              <dockItem.icon.component
                {...dockItem.icon.props}
              />
            {/if}
          </DockItem>
        {/each}
      </div>
          <!-- {/snippet} -->
    </Motion.div>
</div>
