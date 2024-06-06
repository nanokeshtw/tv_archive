<script lang="ts">
  import type { MouseEventHandler } from "svelte/elements";

  export let size: number = 100;

  const handleMouseDown: MouseEventHandler<HTMLDivElement> = (event) => {
    event.preventDefault();
    event.stopPropagation();
    const knob = event.currentTarget;
    const knobInner = knob.querySelector(".knob-inner") as HTMLDivElement;

    const handleMouseMove = (event: MouseEvent) => {
      const { clientX, clientY } = event;
      const { left, top, width, height } = knob.getBoundingClientRect();
      const centerX = left + width / 2;
      const centerY = top + height / 2;
      const angle = Math.atan2(clientY - centerY, clientX - centerX);
      const degrees = (angle * 180) / Math.PI;
      const clampedDegrees = Math.ceil(degrees / 15) * 15;
      knobInner.style.transform = `rotate(${clampedDegrees}deg)`;
    };

    const handleMouseUp = () => {
      window.removeEventListener("mousemove", handleMouseMove);
      window.removeEventListener("mouseup", handleMouseUp);
    };

    window.addEventListener("mousemove", handleMouseMove);
    window.addEventListener("mouseup", handleMouseUp);
  };
</script>

<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
<div
  class="knob"
  style="--size: {size}px;"
  role="progressbar"
  on:mousedown={handleMouseDown}
>
  <div class="knob-inner" />
</div>

<style lang="scss">
  .knob {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: var(--size, 100px);
    height: var(--size, 100px);
    aspect-ratio: 1/1;
    border-radius: 1000px;
    background: url("/radial-circle.png") no-repeat center center;
    background-color: #856229;
    background-size: contain;
    box-shadow:
      -2px -2px 5px rgba(255, 255, 255, 0.1),
      2px 2px 5px rgba(0, 0, 0, 0.5);

    &::before {
      content: "";
      position: absolute;
      width: 80%;
      height: 80%;
      border-radius: 1000px;
      background-color: #967034;
    }

    &-inner {
      position: relative;
      width: 90%;
      height: calc(var(--size, 100px) / 12);
      border-radius: calc(var(--size, 100px) / 60);
      background-color: #be995d;

      &::after {
        content: "";
        position: absolute;
        top: 50%;
        bottom: 50%;
        right: 2%;
        height: 50%;
        width: 100%;
        background: url("/radial-arrow.png") no-repeat center right;
        background-size: contain;
        transform: translateY(-50%);
      }
    }
  }
</style>
