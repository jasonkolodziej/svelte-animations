<script lang="ts">
  import ComponentView from "$lib/luxe/components/codeblock/ComponentView.svelte";
  import { page } from "$app/stores";
  import CodeBlock from "$lib/luxe/components/codeblock/CodeBlock.svelte";
  import { animationExamples } from "$lib/examples/AnimationsExamples";

  let routeID = $derived($page.params.exampleID);
  let comp = $derived(animationExamples.filter((comp) => comp.id == Number(routeID))[0]);
  let fileName =
    $derived(comp.name
      .split(" ")
      .map((k) => {
        let kit = k.charAt(0).toUpperCase();
        let m = kit + k.replace(k[0], "");
        return m;
      })
      .join("") + ".svelte");
</script>

<div class="my-0 md:my-2 mx-2 md:mx-5">
  <a
    href="/examples"
    class="flex items-center gap-1 text-muted-foreground w-fit"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="17"
      height="17"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="1.2"
      stroke-linecap="round"
      stroke-linejoin="round"
      class="lucide lucide-arrow-left mt-px"
      ><path d="m12 19-7-7 7-7" /><path d="M19 12H5" /></svg
    >
    Back
  </a>
  {#key comp}
    <div class="space-y-7">
      <h1 class="text-2xl font-bold mt-4 md:text-3xl capitalize my-6">
        {comp.name}
      </h1>
      <div>
        <ComponentView>
          <comp.component />
        </ComponentView>
      </div>
      <div>
        {#key comp}
          <CodeBlock code={comp.code} {fileName} />
        {/key}
      </div>
    </div>
  {/key}
</div>
