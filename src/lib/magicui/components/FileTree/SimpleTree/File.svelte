<script lang="ts">
  import { run } from 'svelte/legacy';

  import TsImg from "./svgs/ts.svg";
  import SvelteImg from "./svgs/svelte.svg";
  import JsImg from "./svgs/js.svg";
  import Img from "./svgs/image.svg";
  let { name } = $props();
  // All SVG Files are downloaded from
  /*
  Twitter : https://simpleicons.org/?q=twitter
  Svelte : https://svgl.app/?search=svelte
  TS : https://svgl.app/?search=typescript
  Image,folder open, close icons from ; https://lucide.dev/icons/ 
  */

  let allFiles: any = {
    svelte: SvelteImg,
    ts: TsImg,
    js: JsImg,
    png: Img,
  };
  let type = $derived(name.slice(name.lastIndexOf(".") + 1));
  run(() => {
    console.log(type, "Code");
  });
</script>

<span class=" w-fit">
  <img src={allFiles[type]} class=" h-[16px] w-[15px] mt-1" alt={type} />
  {name}</span
>

<style>
  span {
    display: flex;
    align-items: center;
    gap: 3px;
  }
</style>
