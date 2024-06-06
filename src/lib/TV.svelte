<script lang="ts">
  import TvKnob from "./TVKnob.svelte";

  export let hasTV = true;

  const handleZoomInSite = () => {
    const screen = document.getElementById("screen") as HTMLDivElement;
    const scaleX = window.innerWidth / screen.clientWidth;
    const scaleY = window.innerHeight / screen.clientHeight;
    const animation = screen.animate(
      [
        { transform: "scale(1, 1)", zIndex: 1000 },
        {
          transform: `scale(${scaleY}, ${scaleX})`,
          borderRadius: "0px",
          zIndex: 1000,
        },
      ],
      {
        duration: 1000,
        easing: "ease-in-out",
      },
    );
    animation.onfinish = () => {
      hasTV = false;
    };
  };
</script>

<div class="tv-container">
  <div class="outer-box">
    <div class="screen-border">
      <div id="screen" class="screen">
        <slot />
      </div>
    </div>
    <div class="controls">
      <TvKnob size={120} />
      <div class="small-knobs">
        <TvKnob size={90} />
        <TvKnob size={90} />
      </div>
      <div class="dots">
        <button on:click={handleZoomInSite}></button>
        <button></button>
        <button></button>
      </div>
    </div>
  </div>
</div>

<style lang="scss">
  .tv-container {
    height: 100%;
    width: 100%;
    height: 100%;
    padding: 60px 80px 40px;
  }

  .outer-box {
    position: relative;
    flex: 1;
    display: flex;
    height: 100%;
    padding: 20px;
    // linear gradient so it looks like a light source is top right
    background: linear-gradient(135deg, #9a4528, #86391f);
    background-color: #86391f;
    transform-style: preserve-3d;

    &:before,
    &:after {
      content: "";
      position: absolute;
    }
    &:before {
      top: -40px;
      left: 0;
      width: calc(100% + 1px);
      height: 40px;
      background-color: #ab4f31;
      transform-origin: bottom center;
      transform: rotateX(-45deg) skewX(-45deg);
    }
    &:after {
      top: 0;
      left: 100%;
      width: 48px;
      height: 100%;
      background-color: #86391f;
      transform-origin: center left;
      transform: rotateY(-31deg) skewY(-31deg);
    }
  }

  .screen-border {
    flex: 1;
    padding: 48px;
    background: linear-gradient(135deg, #723a15, #673414);
    box-shadow: inset 0 0 20px rgba(#884920, 0.5);
  }

  .screen {
    position: relative;
    height: 100%;
    border-radius: 20vh;
    background-color: #ece6c2;
    box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.5);
    overflow: hidden;

    & :global(.site-container) {
      background-color: unset;
    }

    &::after {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      border-radius: 20vh;
      background: url("/tv-static.gif") center center;
      background-size: 101% 101%;
      opacity: 0.05;
      pointer-events: none;
    }
  }

  .controls {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 40px;
    padding-inline: 38px;
    padding-block: 40px 20px;
    background-color: #a37f45;

    & .dots,
    & .small-knobs {
      margin-top: auto;
    }

    & .small-knobs {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 40px;
    }
  }
</style>
