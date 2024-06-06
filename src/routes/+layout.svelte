<script>
  import Header from "$lib/Header.svelte";
  import Site from "$lib/Site.svelte";
  import Tv from "$lib/TV.svelte";
  import { fade, scale } from "svelte/transition";

  let hasTV = true;

  let rotation = 0;
  setInterval(() => {
    rotation += 0.1;
    rotation %= 360;
  }, 10);
</script>

{#if hasTV}
  <main style="--rotation: {rotation}deg">
    <Tv bind:hasTV>
      <div>
        <Site>
          <slot />
        </Site>
      </div>
    </Tv>
  </main>
{:else}
  <div style="height: 100%;">
    <Site>
      <slot />
    </Site>
  </div>
{/if}

<style lang="scss">
  main {
    position: relative;
    height: 100%;

    &::before {
      content: "";
      position: fixed;
      top: min(-38vw, -38vh);
      left: min(-19vw, -19vh);
      width: max(133vw, 133vh);
      height: max(133vw, 133vh);
      background: url("/bg-rainbow.jpg") no-repeat center center;
      background-size: cover;
      z-index: -1;
      transform: rotate(var(--rotation));
    }
  }
</style>
