<script lang="ts">
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  import Navbar from "$lib/components/dev/Navbar/Navbar.svelte";
  import "../app.css";
  import "./global.css";
  import { ModeWatcher } from "mode-watcher";
  let routeID = $derived($page.url.pathname.split("/"));

  import { resetMode, setMode } from "mode-watcher";
  import NewNavbar from "$lib/components/dev/Navbar/NewNavbar.svelte";
  interface Props {
    children?: import('svelte').Snippet;
  }

  let { children }: Props = $props();
  setMode("dark");
  let pageWidth = $state(0);
</script>

<svelte:window bind:innerWidth={pageWidth} />
<ModeWatcher />
<!-- {#if pageWidth > 1023 && routeID[1] === "examples"}
  <Navbar />
{:else if routeID[1] === ""}
  <Navbar />
{/if} -->
<NewNavbar />
<div>
  {@render children?.()}
</div>
