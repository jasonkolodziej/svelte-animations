<script lang="ts">
    import {
      Motion,
      useMotionValue,
      useTransform,
    } from "svelte-motion";
    let exitX = $state(0);
    const x = useMotionValue(0);
    const scale = useTransform(x, [-150, 0, 150], [0.5, 1, 0.5]);
    const rotate = useTransform(x, [-150, 0, 150], [-45, 0, 45], {
      clamp: false,
    });
  interface Props {
    drag?: any;
    frontCard?: boolean;
    index?: any;
  }

  let { drag = false, frontCard = false, index = $bindable(0) }: Props = $props();
    const variantsFrontCard = {
      animate: { scale: 1, y: 0, opacity: 1 },
      exit: (custom: any) => ({ x: custom, opacity: 0, scale: 0.5 }),
    };
    const variantsBackCard = {
      initial: { scale: 0.3, y: 105, opacity: 0 },
      animate: { scale: 0.75, y: 30, opacity: 0.5 },
    };
    let isFront = $derived(frontCard ? variantsFrontCard : variantsBackCard);
  
    function handleDragEnd(_, info) {
      // console.log("info", info);
      if (info.offset.x < -100) {
        // setExitX(-250);
        exitX = -250;
        //   props.setIndex(index + 1);
        index = index + 1;
      }
      if (info.offset.x > 100) {
        exitX = 250;
        //   props.setIndex(index + 1);
        index = index + 1;
      //   console.log("trigger");
      }
    }
    let i = 0;
  </script>
  
  <!-- Animate Presence Stack -->
  
  <Motion
    style={{
      x,
      rotate,
    }}
    {drag}
    dragConstraints={{ top: 0, right: 0, bottom: 0, left: 0 }}
    variants={isFront}
    initial="initial"
    animate="animate"
    onDragEnd={handleDragEnd}
    exit="exit"
    custom={exitX}
    transition={frontCard
      ? { type: "spring", stiffness: 300, damping: 20 }
      : { scale: { duration: 0.2 }, opacity: { duration: 0.4 } }}
    
  >
    {#snippet children({ motion })}
    <div
        class="w-32 h-32 top-10 bg-white rouned-xl absolute rounded-xl text-black flex justify-center items-center select-none"
        use:motion
      >
        {index}
      </div>
      {/snippet}
</Motion>
  