<script lang="ts">
    import { cn } from "$lib/utils";
    import { useViewportScroll,useElementScroll } from "svelte-motion";
    import Word from "./Word.svelte";
    
  interface Props {
    class?: any;
    text?: string;
  }

  let { class: className = "", text = "Hello Everyone Svelte is Fun" }: Props = $props();
    let words = text.split(" ");
    // let { scrollYProgress } = useViewportScroll();
    let val = $state(useElementScroll());
    let icode = val.scrollYProgress;
  </script>
  
  <div bind:this={val.ref} class="scroller">
    <div class={cn("relative z-10 h-[200vh]", className)}>
      <div
        class="sticky top-0 mx-auto flex h-[10%] max-w-4xl items-center bg-transparent px-[1rem] py-[5rem]"
      >
        <p
          class={"flex flex-wrap p-5 text-2xl font-bold text-black/20 dark:text-white/20 md:p-8 md:text-3xl lg:p-10 lg:text-4xl xl:text-5xl"}
        >
          {#each words as item, i}
            <Word
              progress={icode}
              range={[i, i + 1]}
              wordsLen={words.length}
            >
              {item}
            </Word>
          {/each}
        </p>
      </div>
    </div>
  </div>
  
  <style>
    .scroller {
      position: absolute;
      overflow: scroll;
      display: inline-block;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
    }
  </style>
  