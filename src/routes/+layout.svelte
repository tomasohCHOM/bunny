<svelte:head>
  <title>Threlte</title>
</svelte:head>

<div class="scene">
  <slot />
</div>

<style>
  .scene {
    position: absolute;
    inset: 0;
    background: radial-gradient(hsl(220 14% 20%), hsl(220 20% 10%));
  }
</style>
