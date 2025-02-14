<script lang="ts">
    import { onMount } from 'svelte';
    import Particles from "@tsparticles/svelte";
    import { tweened } from 'svelte/motion';
    
    
  interface Props {
    id: any;
    class?: string;
    background?: string;
    minSize?: number;
    maxSize?: number;
    speed?: number;
    particleColor?: string;
    particleDensity?: number;
  }

  let {
    id,
    class: className = '',
    background = '#0d47a1',
    minSize = 1,
    maxSize = 3,
    speed = 4,
    particleColor = '#ffffff',
    particleDensity = 120
  }: Props = $props();
  
    let init = $state(false);
    const opacity = tweened(0, { duration: 1000 });
  
    onMount(() => {
      // Load particles engine with slim configuration
      init = true;
      opacity.set(1);  // Animate opacity to fade-in effect
    });
  
    const particlesLoaded = () => {
      opacity.set(1);  // Ensure opacity is set after particles are loaded
    };
  </script>
  
  <div class={className} style="opacity: {$opacity}">
    {#if init}
      <Particles
        id={id}
        options={{
          background: { color: { value: background } },
          fullScreen: { enable: false, zIndex: 1 },
          fpsLimit: 120,
          interactivity: {
            events: {
              onClick: { enable: true, mode: "push" },
              onHover: { enable: false, mode: "repulse" },
              resize: true,
            },
            modes: {
              push: { quantity: 4 },
              repulse: { distance: 200, duration: 0.4 },
            },
          },
          particles: {
            color: { value: particleColor },
            move: {
              enable: true,
              speed: { min: 0.1, max: 1 },
            },
            size: {
              value: { min: minSize, max: maxSize },
            },
            opacity: {
              value: { min: 0.1, max: 1 },
              animation: {
                enable: true,
                speed: speed,
                sync: false,
              },
            },
            number: {
              density: { enable: true, width: 400, height: 400 },
              value: particleDensity,
            },
          },
          detectRetina: true,
        }}
        on:particlesLoaded={particlesLoaded}
      />
    {/if}
  </div>
  
  <style>
    .h-full { height: 100%; }
    .w-full { width: 100%; }
  </style>
  