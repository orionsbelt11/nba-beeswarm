<script>
  export let xScale;
  export let height;

  $: ticks = xScale.ticks(10);

  console.log(ticks)
  
</script>

<g class="axis x" transform="translate(0, {height})">
  {#each ticks as tick}
    <g class="tick" transform="translate({xScale(tick)}, 0)">
      <text x={0} y={6} dy={9} text-anchor="middle">{tick}</text>
      <line x1={0} x2={0} y1={-4} y2={2} stroke='#8f8f8f'/>
    </g>
  {/each}
</g>

<style>
</style>
