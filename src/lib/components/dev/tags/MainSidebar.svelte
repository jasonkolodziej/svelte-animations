<script lang="ts">
  import { page } from "$app/stores";
  import { navs } from "$lib";
  import Separator from "$lib/components/ui/separator/separator.svelte";
  import { animationExamples } from "$lib/examples/AnimationsExamples";
  import { onMount } from "svelte";
  import { blur, slide } from "svelte/transition";
  let { componentsNav = [
    {
      id: 1,
      heading: "Getting Started",
      sub: [
        {
          name: "Browse Components",
          link: "/examples",
        },
      ],
    },
    {
      id: 2,
      heading: "Components",
      sub: animationExamples,
    },
  ], children } = $props();

  let mobileMenu = $state(true);
  let isLoading = $state(false);
  let routeID = $derived($page.url.pathname);
  onMount(() => {
    isLoading = true;
  });
</script>

<div>
  <!-- Off-canvas menu for mobile, show/hide based on off-canvas menu state. -->
  <div
    class="relative lg:hidden transition-opacity ease-linear duration-300 {mobileMenu
      ? 'opacity-0 z-10'
      : 'opacity-100 z-50 '} "
    role="dialog"
    aria-modal="true"
  >
    <div
      class="{mobileMenu
        ? '-translate-x-full'
        : 'translate-x-0'} transition-opacity ease-linear duration-300 fixed inset-0 dark:bg-background"
    ></div>

    <div
      class="{mobileMenu
        ? '-translate-x-full'
        : 'translate-x-0'} fixed inset-0 flex
        transition ease-in-out duration-300 transform
        "
    >
      <div
        class="{mobileMenu
          ? 'opacity-0'
          : 'opacity-100'} ease-in-out duration-300 relative mr-16 flex w-full max-w-xs flex-1"
      >
        <div class="absolute left-full top-0 flex w-16 justify-center pt-5">
          <button
            onclick={() => {
              mobileMenu = !mobileMenu;
            }}
            type="button"
            class="-m-2.5 p-2.5"
          >
            <span class="sr-only">Close sidebar</span>
            <svg
              class="h-6 w-6 text-white"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>

        <!-- Sidebar component, swap this element with another sidebar if you like -->
        <div class="flex grow flex-col overflow-y-auto px-6 m-0 p-0">
          <div
            class="flex h-16 shrink-0 items-center border-b border-primary/50"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="22"
              height="22"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.4"
              stroke-linecap="round"
              stroke-linejoin="round"
              class="lucide lucide-tornado"
              ><path d="M21 4H3" /><path d="M18 8H6" /><path
                d="M19 12H9"
              /><path d="M16 16h-6" /><path d="M11 20H9" /></svg
            >
            <span class="ml-2 overpass-mono mt-px">Svelte Animations</span>
          </div>
          <nav class="flex flex-1 flex-col">
            {#key mobileMenu}
              <div class="transition-all duration-150" transition:slide>
                {#each navs as item}
                  <a
                    href={item.link}
                    class="group {item.link === routeID
                      ? 'text-primary font-medium rounded-md'
                      : 'text-primary/60'} flex gap-x-3 p-2 text-sm leading-6"
                  >
                    {item.name}
                  </a>
                {/each}
              </div>
            {/key}
            <ul role="list" class="flex flex-1 flex-col gap-y-7 mt-4">
              <li>
                <ul role="list" class="-mx-2">
                  {#each componentsNav as cnavs}
                    <div class="mb-4">
                      <div class="font-medium">
                        {cnavs.heading}
                      </div>
                      {#each cnavs.sub as item}
                        <li>
                          <a
                            onclick={() => {
                              mobileMenu = !mobileMenu;
                            }}
                            href={item.link}
                            class="group {item.link === routeID
                              ? 'text-primary'
                              : 'text-primary/60'} flex gap-x-3 rounded-md p-2 text-sm leading-6"
                          >
                            {item.name}
                          </a>
                        </li>
                      {/each}
                    </div>
                  {/each}
                </ul>
              </li>
            </ul>
          </nav>
        </div>
      </div>
    </div>
  </div>

  <!-- in:fly={{ x: -200, duration: 600 }} -->
  <!-- Static sidebar for desktop -->
  {#if isLoading}
    <div
      class="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-64 lg:flex-col mt-16"
    >
      <!-- Sidebar component, swap this element with another sidebar if you like -->
      <div
        class="flex grow flex-col gap-y-0 overflow-y-auto dark:border-primary/40 dark:bg-background bg-white px-6"
      >
        <nav class="flex flex-1 flex-col mb-32">
          <a href="/" class="font-bold text-xl mx-1 my-3">Svelte Animations</a>
          <Separator class="mb-2" />
          <ul role="list" class="flex flex-1 flex-col">
            {#each componentsNav as item}
              <li>
                <ul role="list" class="">
                  <li class="mt-4">
                    <div
                      class="text-primary/95 font-semibold text-md leading-6 p-2"
                    >
                      {item.heading}
                    </div>
                  </li>
                  {#each item.sub as subItem}
                    <li>
                      <a
                        href={subItem.link}
                        class="group {subItem.link == routeID
                          ? 'text-primary bg-neutral-900 border-border font-medium'
                          : 'text-primary/60 '} capitalize flex gap-x-3 p-2 text-sm leading-6 select-none px-3 py-1.5 mb-0.5 border border-transparent rounded-sm hover:bg-neutral-900 transition-all duration-300"
                      >
                        {subItem.name}
                      </a>
                    </li>
                  {/each}
                </ul>
              </li>
            {/each}
          </ul>
        </nav>
      </div>
    </div>
  {/if}

  <div
    class="sticky top-0 z-40 flex items-center gap-x-6 dark:bg-background border-b bg-white backdrop-blur-md px-4 py-4 shadow-sm sm:px-6 lg:hidden"
  >
    <button
      onclick={() => (mobileMenu = !mobileMenu)}
      type="button"
      class="-m-2.5 p-2.5 text-primary/70 lg:hidden"
    >
      <span class="sr-only">Open sidebar</span>
      <svg
        class="h-6 w-6"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        aria-hidden="true"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
        />
      </svg>
    </button>
    <div class="flex-1 text-sm font-semibold leading-6 text-primary">
      Svelte Framer Motion
    </div>
  </div>

  <main class="py-6 lg:pl-60 dark:bg-background min-h-screen">
    <div class="px-4 sm:px-6 lg:px-8">
      {@render children?.()}
    </div>
  </main>
</div>
