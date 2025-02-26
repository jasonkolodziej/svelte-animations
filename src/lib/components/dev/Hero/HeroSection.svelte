<script lang="ts">
  import Badge from "$lib/components/ui/badge/badge.svelte";
  import Button from "$lib/components/ui/button/button.svelte";
  import DotBackground from "$lib/components/ui/GridDotBg/DotBackground.svelte";
  import GradientLine from "$lib/luxe/components/codeblock/GradientLine.svelte";
  import { onMount } from "svelte";
  let stars = $state(0);
  let getStarsCount = async () => {
    let res = await fetch(
      "https://api.github.com/repos/SikandarJODD/svelte-animations"
    );
    let data = await res.json();
    let starsCount = data.stargazers_count;
    return starsCount;
  };
  let navItems = [
    { name: "Luxe Components", href: "/luxe" },
    { name: "Framer", href: "/learnings" },
    { name: "Examples", href: "/examples" },
    { name: "Magic UI", href: "/magic" },
  ];
  onMount(async () => {
    stars = await getStarsCount();
  });
</script>

<DotBackground>
  <div
    class="relative flex h-[97vh] md:h-[92vh] overflow-hidden rounded-md px-4 antialiased md:items-center md:justify-center lg:px-32"
  >
    <!-- <Spotlight className="-top-40 left-0 md:left-32 md:-top-40"  /> -->
    <div class=" z-10 mx-auto w-full max-w-7xl p-4 pt-20 md:pt-0">
      <h1
        class="bg-opacity-50 pb-2 bg-gradient-to-r from-neutral-100 via-neutral-300 to-neutral-500 bg-clip-text text-center text-4xl font-bold text-transparent md:text-7xl"
      >
        Svelte Animation Components
      </h1>
      <p
        class="mx-auto mt-2 max-w-lg text-center text-base md:text-lg font-normal text-neutral-300"
      >
        Free Components, Build using Tailwind CSS, <a
          href="https://svelte-motion.gradientdescent.de"
          class=" text-teal-300">Svelte Motion</a
        >
      </p>
      <div class="flex justify-center items-center mt-4">
        {#if stars > 0}
          <Button
            size="sm"
            target="_blank"
            variant="outline"
            href="https://github.com/SikandarJODD/svelte-animations"
            ><svg
              viewBox="0 0 256 250"
              width="20"
              height="20"
              fill="currentColor"
              xmlns="http://www.w3.org/2000/svg"
              preserveAspectRatio="xMidYMid"
              class="mr-1.5"
            >
              <path
                d="M128.001 0C57.317 0 0 57.307 0 128.001c0 56.554 36.676 104.535 87.535 121.46 6.397 1.185 8.746-2.777 8.746-6.158 0-3.052-.12-13.135-.174-23.83-35.61 7.742-43.124-15.103-43.124-15.103-5.823-14.795-14.213-18.73-14.213-18.73-11.613-7.944.876-7.78.876-7.78 12.853.902 19.621 13.19 19.621 13.19 11.417 19.568 29.945 13.911 37.249 10.64 1.149-8.272 4.466-13.92 8.127-17.116-28.431-3.236-58.318-14.212-58.318-63.258 0-13.975 5-25.394 13.188-34.358-1.329-3.224-5.71-16.242 1.24-33.874 0 0 10.749-3.44 35.21 13.121 10.21-2.836 21.16-4.258 32.038-4.307 10.878.049 21.837 1.47 32.066 4.307 24.431-16.56 35.165-13.12 35.165-13.12 6.967 17.63 2.584 30.65 1.255 33.873 8.207 8.964 13.173 20.383 13.173 34.358 0 49.163-29.944 59.988-58.447 63.157 4.591 3.972 8.682 11.762 8.682 23.704 0 17.126-.148 30.91-.148 35.126 0 3.407 2.304 7.398 8.792 6.14C219.37 232.5 256 184.537 256 128.002 256 57.307 198.691 0 128.001 0Zm-80.06 182.34c-.282.636-1.283.827-2.194.39-.929-.417-1.45-1.284-1.15-1.922.276-.655 1.279-.838 2.205-.399.93.418 1.46 1.293 1.139 1.931Zm6.296 5.618c-.61.566-1.804.303-2.614-.591-.837-.892-.994-2.086-.375-2.66.63-.566 1.787-.301 2.626.591.838.903 1 2.088.363 2.66Zm4.32 7.188c-.785.545-2.067.034-2.86-1.104-.784-1.138-.784-2.503.017-3.05.795-.547 2.058-.055 2.861 1.075.782 1.157.782 2.522-.019 3.08Zm7.304 8.325c-.701.774-2.196.566-3.29-.49-1.119-1.032-1.43-2.496-.726-3.27.71-.776 2.213-.558 3.315.49 1.11 1.03 1.45 2.505.701 3.27Zm9.442 2.81c-.31 1.003-1.75 1.459-3.199 1.033-1.448-.439-2.395-1.613-2.103-2.626.301-1.01 1.747-1.484 3.207-1.028 1.446.436 2.396 1.602 2.095 2.622Zm10.744 1.193c.036 1.055-1.193 1.93-2.715 1.95-1.53.034-2.769-.82-2.786-1.86 0-1.065 1.202-1.932 2.733-1.958 1.522-.03 2.768.818 2.768 1.868Zm10.555-.405c.182 1.03-.875 2.088-2.387 2.37-1.485.271-2.861-.365-3.05-1.386-.184-1.056.893-2.114 2.376-2.387 1.514-.263 2.868.356 3.061 1.403Z"
              />
            </svg>
            {stars}</Button
          >
        {/if}
      </div>

      <div
        class="relative flex flex-col my-4 md:w-[290px] mx-auto p-4 rounded-xl border justify-center items-center gap-3 bg-neutral-900/15"
      >
        <div class="w-full">
          <Button
            href="/magic"
            variant="secondary"
            class="flex justify-center gap-3 w-full"
            >Svelte Magic UI
            <!-- <Badge>New</Badge> -->
          </Button>
        </div>
        <div class="grid grid-cols-2 md:grid-cols-5 gap-3">
          <Button href="/examples" variant="outline" class="md:col-span-2"
            >Examples</Button
          >
          <Button href="/learnings" variant="outline" class="md:col-span-3"
            >Framer Learnings</Button
          >
        </div>
        <div class="grid grid-cols-2 md:grid-cols-5 gap-3">
          <Button href="/luxe" variant="animated" class="md:col-span-3"
            >Luxe Components</Button
          >
          <Button href="/in" variant="shine" class="md:col-span-2"
            >Indie UI</Button
          >
        </div>
        <div class="w-full">
          <Button
            href="/a/components/bento-grid"
            variant="secondary"
            class="flex justify-center gap-3 w-full"
            >Svelte Acterenity UI
            <Badge>New</Badge>
          </Button>
        </div>
      </div>
      <div class="flex justify-center items-center">
        <div
          class="absolute bottom-5 flex justify-center items-center flex-col"
        >
          <a
            href="https://github.com/SikandarJODD"
            class="font-mono text-neutral-300 underline underline-offset-2"
          >
            Build by Sikandar.S.Bhide
          </a>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="1.4"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="lucide lucide-chevron-down animate-bounce mt-2"
            ><path d="m6 9 6 6 6-6" /></svg
          >
        </div>
      </div>
    </div>
  </div>
</DotBackground>
