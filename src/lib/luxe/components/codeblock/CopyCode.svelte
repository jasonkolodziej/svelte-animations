<script lang="ts">
  interface Props {
    code?: string;
  }

  let { code = "" }: Props = $props();
  let isCopied = $state(false);
  let handleCopy = () => {
    navigator.clipboard.writeText(code);
    isCopied = true;
    setTimeout(() => {
      isCopied = false;
    }, 1500);
  };
</script>

<button
  onclick={handleCopy}
  class="rounded-full py-1.5 w-[70px] border bg-neutral-900 border-border {isCopied
    ? 'bg-green-900/30 border-green-400/50 '
    : ''} "
>
  <span
    class="flex items-center justify-center gap-1.5 {isCopied
      ? 'text-green-400/70'
      : 'text-neutral-200'} text-xs font-medium"
  >
    {isCopied ? "Copied!" : "Copy"}
  </span>
</button>
