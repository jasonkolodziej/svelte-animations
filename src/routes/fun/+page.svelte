<script>
  import { page } from "$app/stores";
  import Badge from "$lib/components/ui/badge/badge.svelte";
  import Bento4Variant1 from "$lib/indieui/components/bentogrids/bento4/bento4Variant1.svelte";
  import Bento4Variant2 from "$lib/indieui/components/bentogrids/bento4/bento4Variant2.svelte";
  import Bento4Variant4 from "$lib/indieui/components/bentogrids/bento4/bento4Variant4.svelte";
  import Bentro4Variant3 from "$lib/indieui/components/bentogrids/bento4/bentro4Variant3.svelte";
  import Bento5Variant1 from "$lib/indieui/components/bentogrids/bento5/Bento5Variant1.svelte";
  import Bento5Variant2 from "$lib/indieui/components/bentogrids/bento5/Bento5Variant2.svelte";
  import Bento5Variant3 from "$lib/indieui/components/bentogrids/bento5/Bento5Variant3.svelte";
  import Bento5Variant4 from "$lib/indieui/components/bentogrids/bento5/Bento5Variant4.svelte";
  import Bento6Variant1 from "$lib/indieui/components/bentogrids/bento6/Bento6Variant1.svelte";
  import Bento6variant2 from "$lib/indieui/components/bentogrids/bento6/Bento6variant2.svelte";
  import Bento6Variant3 from "$lib/indieui/components/bentogrids/bento6/Bento6Variant3.svelte";
  import Bento6Variant4 from "$lib/indieui/components/bentogrids/bento6/Bento6Variant4.svelte";
  import CardImage1 from "$lib/indieui/components/cards/cardimages/CardImage1.svelte";
  import CardImage2 from "$lib/indieui/components/cards/cardimages/CardImage2.svelte";
  import CardImage3 from "$lib/indieui/components/cards/cardimages/CardImage3.svelte";
  import CardImage4 from "$lib/indieui/components/cards/cardimages/CardImage4.svelte";
  import MultiLayerCard1 from "$lib/indieui/components/cards/muiltlayers/MultiLayerCard1.svelte";
  import MultiLayerCard2 from "$lib/indieui/components/cards/muiltlayers/MultiLayerCard2.svelte";
  import MultiLayerCard3 from "$lib/indieui/components/cards/muiltlayers/MultiLayerCard3.svelte";
  import MultiLayerCard4 from "$lib/indieui/components/cards/muiltlayers/MultiLayerCard4.svelte";
  import SimpleCardVariant1 from "$lib/indieui/components/cards/simple/SimpleCardVariant1.svelte";
  import SimpleCardVariant2 from "$lib/indieui/components/cards/simple/SimpleCardVariant2.svelte";
  import SimpleCardVariant3 from "$lib/indieui/components/cards/simple/SimpleCardVariant3.svelte";
  import SimpleCardVariant4 from "$lib/indieui/components/cards/simple/SimpleCardVariant4.svelte";
  import SimpleCardVariant5 from "$lib/indieui/components/cards/simple/SimpleCardVariant5.svelte";
  import SimpleCardVariant6 from "$lib/indieui/components/cards/simple/SimpleCardVariant6.svelte";
  import SkeletonVariant1 from "$lib/indieui/components/loaders/skeleton/skeletonVariant1.svelte";
  import SkeletonVariant2 from "$lib/indieui/components/loaders/skeleton/skeletonVariant2.svelte";
  import HeaderExample from "$lib/indieui/components/other/header/examples/HeaderExample.svelte";
  import Separator from "$lib/indieui/components/other/separator/Separator.svelte";
  import { fade, slide } from "svelte/transition";
  let routeId = $derived($page.url.pathname);
  let innerWidth = $state(0);
</script>

<svelte:window bind:innerWidth />
{#if innerWidth > 600}
  <HeaderExample />
{/if}
<div
  class="flex justify-center items-center text-center w-full min-h-14 bg-gradient-to-r from-transparent via-zinc-900/70 to-transparent backdrop-blur-sm text-primary/60 {routeId ===
  '/fun'
    ? 'sticky top-0'
    : ''}  z-20"
>
  
  <p>
    Visit <a href="/magic" class="text-primary">Magic UI</a>
    and
    <a href="/magic" class=" text-primary">Luxe Components</a> for Amazing components.
  </p>
</div>
<div class="w-full flex p-4 flex-col md:flex-row gap-2 mt-0">
  <div
    class="relative group flex justify-center items-center min-h-[60vh] w-full md:w-1/4 flex-col border border-dashed gap-8 p-6 md:p-0"
  >
    <div class="absolute top-3 left-3 group-hover:flex hidden">
      <Badge href="/in/skeleton" variant="default">Skeleton</Badge>
    </div>
    <SkeletonVariant1 />
    <SkeletonVariant2 />
  </div>
  <div class="w-full md:w-3/4 group">
    <div class="flex p-4 gap-2 w-full h-fit border border-dashed">
      <div class="w-1/2 h-fit relative">
        <div class="absolute top-3 left-3 group-hover:flex hidden">
          <Badge href="/in/bento-4" variant="default">Bento 4</Badge>
        </div>
        <Bento4Variant1 />
      </div>
      <div class="w-1/2 h-fit">
        <Bento4Variant2 />
      </div>
    </div>
    <div
      class="flex p-4 gap-2 w-full h-fit border-r border-b border-l border-dashed"
    >
      <div class="w-full">
        <Bentro4Variant3 />
      </div>
    </div>
  </div>
</div>
<!-- <div class="w-full px-4 flex flex-col md:flex-row gap-2">
  <div class="w-2/5 p-4 border border-dashed">
    <Bento4Variant4 />
  </div>
  <div class="w-3/5 p-4 border h-full border-dashed">
    <Bento5Variant2 />
  </div>
</div> -->
<!-- <div class="w-full px-4 flex flex-col md:flex-row gap-2 mt-4">
  <div class="w-1/2 p-4 border border-dashed">
    <Bento5Variant1 />
  </div>
  <div class="w-1/2 p-4 border h-full border-dashed">
    <Bento5Variant3 />
  </div>
</div>
<div class="w-full px-4 flex flex-col md:flex-row gap-2 mt-4">
  <div class="w-full md:w-2/5 p-4 border border-dashed">
    <Bento5Variant4 />
  </div>
  <div class="w-full md:w-3/5 p-4 border h-full border-dashed">
    <Bento6variant2 />
  </div>
</div> -->
<!-- <div class="w-full px-4 flex flex-col md:flex-row gap-2 mt-4">
  <div class="w-full md:w-3/5 mx-auto p-4 border border-dashed">
    <Bento6Variant3 />
  </div>
</div> -->

<!-- Card with Images -->
<div
  class="w-full flex flex-col items-center md:flex-row min-h-64 gap-4 bg-zinc-950 px-2 md:px-10 py-2 md:py-5"
>
  <div
    class="w-full md:w-1/2 min-h-64 relative items-center group p-3 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-3 left-3 group-hover:flex hidden">
      <Badge href="/in/cards-image" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <CardImage1 />
    </div>
  </div>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-3 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-3 left-3 group-hover:flex hidden">
      <Badge href="/in/cards-image" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <CardImage2 />
    </div>
  </div>
</div>
<!-- Card with Images Variant 3,4 -->
<div
  class="w-full flex flex-col items-center md:flex-row min-h-64 gap-4 bg-zinc-950 px-2 md:px-10 py-2 md:py-5"
>
  <div
    class="w-full md:w-1/2 relative group min-h-64 items-center p-3 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-3 left-3 group-hover:flex hidden">
      <Badge href="/in/cards-image" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <CardImage3 />
    </div>
  </div>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-3 md:p-6 border border-dashed flex justify-center"
  >
    <div class="absolute top-3 left-3 group-hover:flex hidden">
      <Badge href="/in/cards-image" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <CardImage4 />
    </div>
  </div>
</div>

<!-- Simple Cards -->

<div
  class="w-full flex flex-col items-center md:flex-row min-h-64 gap-4 bg-zinc-950 px-2 md:px-10 md:py-5"
>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-4 md:p-0 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-simple" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <SimpleCardVariant1 />
    </div>
  </div>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-4 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-simple" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <SimpleCardVariant2 />
    </div>
  </div>
</div>

<div
  class="w-full flex flex-col items-center md:flex-row min-h-64 gap-4 bg-zinc-950 px-2 md:px-10 md:py-5"
>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-3 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-simple" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <SimpleCardVariant3 />
    </div>
  </div>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-3 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-simple" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <SimpleCardVariant4 />
    </div>
  </div>
</div>

<div
  class="w-full flex flex-col items-center md:flex-row min-h-64 gap-4 bg-zinc-950 px-2 md:px-10 md:py-5"
>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-3 md:p-10 border border-dashed flex justify-center dark:bg-zinc-900/50"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-simple" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <SimpleCardVariant5 />
    </div>
  </div>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-2 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-simple" variant="default">Cards</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <SimpleCardVariant6 />
    </div>
  </div>
</div>

<!-- Multi Layer Cards -->
<div
  class="w-full flex flex-col items-center md:flex-row min-h-64 gap-4 bg-zinc-950 px-2 md:px-10 md:py-5"
>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-5 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-multi-layers" variant="default">Layers</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <MultiLayerCard4 />
    </div>
  </div>
  <div
    class="w-full md:w-1/2 min-h-64 items-center relative group p-3 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-multi-layers" variant="default">Layers</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <MultiLayerCard1 />
    </div>
  </div>
</div>

<!--  Muilt Layer Card 2,3 -->
<div
  class="w-full flex flex-col items-center md:flex-row min-h-64 gap-4 bg-zinc-950 px-2 md:px-10 py-2 md:py-5"
>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-2 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-multi-layers" variant="default">Layers</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <MultiLayerCard3 />
    </div>
  </div>
  <div
    class="w-full md:w-1/2 min-h-64 relative group items-center p-2 md:p-10 border border-dashed flex justify-center"
  >
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/cards-multi-layers" variant="default">Layers</Badge>
    </div>
    <div class="w-full md:w-[80%]">
      <MultiLayerCard2 />
    </div>
  </div>
</div>

<!-- Separators -->
<div
  class="flex justify-center relative group items-center w-full min-h-64 px-20 flex-col gap-10 my-6"
>
  <div class="absolute top-2 left-2/5 group-hover:flex hidden">
    <Badge href="/in/separator" variant="default">Separator</Badge>
  </div>
  <Separator gradient={true} />
  <Separator />
  <Separator gradient={true}>
    {#snippet label()}
        <div  class="px-2">Section</div>
      {/snippet}
  </Separator>
  <Separator>
    {#snippet label()}
        <div  class="px-2">Section</div>
      {/snippet}
  </Separator>
  <Separator>
    {#snippet label()}
        <div  class="border px-4 py-1 rounded-full">Section</div>
      {/snippet}
  </Separator>
  <Separator>
    {#snippet label()}
        <div  class="border px-4 py-1 rounded-full border-dashed">
        Section
      </div>
      {/snippet}
  </Separator>
  <Separator gradient={true}>
    {#snippet label()}
        <div  class="border px-2 py-2 rounded-full">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-plus"
          ><path d="M5 12h14" /><path d="M12 5v14" /></svg
        >
      </div>
      {/snippet}
  </Separator>
</div>

<!-- Bento Grid  6-->
<div class="hidden md:flex w-full px-4 flex-col md:flex-row gap-2 mt-4">
  <div class="w-full md:w-1/2 p-4 relative group border border-dashed">
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/bento-6" variant="default">Bento 6</Badge>
    </div>
    <Bento6Variant1 />
  </div>
  <div class="w-full md:w-1/2 p-4 border border-dashed relative group">
    <div class="absolute top-2 left-2 group-hover:flex hidden">
      <Badge href="/in/bento-6" variant="default">Bento 6</Badge>
    </div>
    <Bento6Variant4 />
  </div>
</div>
<div
  class="flex justify-center items-center text-center w-full min-h-14 text-primary/60 bg-zinc-900 mt-3"
>
  <p>
    Visit <a href="/magic" class="text-primary">Magic UI</a>
    and
    <a href="/magic" class=" text-primary">Luxe Components</a> for Amazing components
  </p>
</div>
