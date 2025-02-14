<script lang="ts">
    interface Props {
        children?: import('svelte').Snippet;
    }

    let { children }: Props = $props();
</script>

<div>
    <h1 class="font-bold text-2xl md:text-3xl mb-2">
        {@render children?.()}
    </h1>
</div>