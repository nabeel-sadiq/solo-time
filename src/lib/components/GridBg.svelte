<script>
  let { children } = $props();
</script>

<div
  class="relative flex items-center justify-center overflow-hidden bg-black"
>
  <div class="absolute inset-0 animated-grid"></div>
  <div class="relative text-white text-4xl font-bold drop-shadow-lg">
    {@render children?.()}
  </div>
</div>

<style>
  @keyframes move-grid {
    0% {
      background-position: 0 0;
    }
    100% {
      background-position: 50px 50px;
    }
  }

  .animated-grid {
    background-size: 50px 50px;
    background-image: linear-gradient(
        to right,
        rgba(255, 255, 255, 0.1) 1px,
        transparent 1px
      ),
      linear-gradient(to bottom, rgba(255, 255, 255, 0.1) 1px, transparent 1px);
    animation: move-grid 8s linear infinite;
  }
</style>
