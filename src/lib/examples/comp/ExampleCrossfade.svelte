<script lang="ts">
    import { cubicInOut, cubicOut, quintInOut } from "svelte/easing";
    import { crossfade, scale, fade, slide, fly, blur } from "svelte/transition";
    let layout = $state("layouta");
  
    let [send, receive] = crossfade({
      duration: 400,
    });
  </script>
  
  <div class="w-full h-full flex justify-center items-center flex-col md:my-44">
    {#if layout === "layouta"}
      <!-- svelte-ignore a11y_click_events_have_key_events -->
      <!-- svelte-ignore a11y_no_static_element_interactions -->
      <div
        onclick={() => {
          layout = "layoutb";
        }}
        class="bg-lime-100 p-4 rounded-3xl layouta w-fit h-fit overflow-hidden"
        in:receive={{ key: "layouta" }}
        out:send={{ key: "layouta" }}
      >
        <div
          class="imgTag"
          in:receive={{ key: "imgTag" }}
          out:send={{ key: "imgTag" }}
        >
          <img
            src="https://i.pinimg.com/564x/b3/7c/fa/b37cfa52ac8e142ffe42772712f6e33d.jpg"
            alt="Saturn Art"
            class="w-56 h-56 rounded-2xl"
          />
        </div>
        <div class="mt-2 px-2 flex flex-col">
          <h1
            class="font-bold text-lg md:text-lg heading text-gray-900"
            in:receive={{ key: "heading" }}
            out:send={{ key: "heading" }}
          >
            Mumbai City
          </h1>
          <p
            class="text-xs sm:text-sm w-52  para text-gray-700"
            in:receive={{ key: "para" }}
            out:send={{ key: "para" }}
          >
            Hello Devs, welcome to our Website
          </p>
        </div>
      </div>
    {:else if layout === "layoutb"}
      <!-- svelte-ignore a11y_click_events_have_key_events -->
      <!-- svelte-ignore a11y_no_static_element_interactions -->
      <div
        onclick={() => {
          layout = "layouta";
        }}
        class="bg-lime-100 p-2.5 md:p-4 rounded-3xl layouta flex gap-1 md:gap-3 w-fit h-fit overflow-hidden"
        in:receive={{ key: "layouta" }}
        out:send={{ key: "layouta" }}
      >
        <div
          class="imgTag"
          in:receive={{ key: "imgTag" }}
          out:send={{ key: "imgTag" }}
        >
          <img
            src="https://i.pinimg.com/564x/b3/7c/fa/b37cfa52ac8e142ffe42772712f6e33d.jpg"
            alt="Saturn Art"
            class="w-36 h-32 md:w-64 md:h-64 rounded-2xl"
          />
        </div>
        <div class="mt-2 px-1 md:px-2 flex flex-col">
          <h1
            class="font-bold text-lg md:text-2xl heading text-gray-900"
            in:receive={{ key: "heading" }}
            out:send={{ key: "heading" }}
          >
            Mumbai City
          </h1>
          <p
            class="text-xs md:text-sm w-full para text-gray-700"
            in:receive={{ key: "para" }}
            out:send={{ key: "para" }}
          >
            Yoo devs, Howw you doing?
          </p>
        </div>
      </div>
    {/if}
  </div>
  
  <style>
    .layouta {
      position: absolute;
    }
  </style>