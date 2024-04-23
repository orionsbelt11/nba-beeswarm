<script>
  export let yScale;
  export let width;

  $: yTicks = yScale.ticks(3);
</script>

<g class="axis y">
  {#each yTicks as tick, index}
    <g class="tick" transform="translate(0, {yScale(tick)})">
      <text y={4} x={-20}>{index === 0 ? "" : tick}</text>
      <line x1={-10} x2={width} y1={-3} y2={-3} stroke={index === 0 ? '#8f8f8f' : "#00000000"}></line>
    </g>
  {/each}
</g>

<style>

</style>
