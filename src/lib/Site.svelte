<script lang="ts">
  import Header from "./Header.svelte";
</script>

<div class="site-container">
  <div class="site">
    <Header />
    <slot />
  </div>
</div>

<style lang="scss">
  .site {
    &-container {
      background-color: #ece6c2;
      height: 100%;
    }

    --padding-inline: 1rem;
    --content-max-width: calc(100% - 240px);
    --breakout-max-width: calc(100% - 120px);
    --breakout-size: calc(
      (var(--breakout-max-width) - var(--content-max-width)) / 2
    );

    display: grid;
    grid-template-columns:
      [full-width-start] minmax(var(--padding-inline), 1fr)
      [breakout-start] minmax(0, var(--breakout-size))
      [content-start] min(
        100% - (var(--padding-inline) * 2),
        var(--content-max-width)
      )
      [content-end]
      minmax(0, var(--breakout-size)) [breakout-end]
      minmax(var(--padding-inline), 1fr) [full-width-end];

    & > :global(:not(.breakout, .full-width)),
    & :global(.section) > :global(:not(.breakout, .full-width)) {
      grid-column: content;
    }

    & > :global(.breakout) {
      grid-column: breakout;
    }

    & > :global(.full-width) {
      grid-column: full-width;
    }

    & > :global(.section) {
      display: grid;
      grid-template-columns: inherit;
    }

    & :global(img.full-width) {
      width: 100%;
      max-height: 45vh;
      object-fit: cover;
    }
  }
</style>
