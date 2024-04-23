<script>
  import data from "$data/outputs/players.js"
  import { scaleLinear, scaleBand, scaleOrdinal } from "d3-scale";
  import { max } from "d3-array";
  import { forceSimulation, forceX, forceY, forceCollide } from "d3-force";
  import { mean, rollups } from "d3-array";
  import AxisX from "$components/AxisX.svelte"
  import AxisY from "$components/AxisY.svelte"
  import Legend from "$components/Legend.svelte"
  import Tooltip from "$components/Tooltip.svelte";
  console.log(data)

//chart scaffolding

  let width = 400,
      height = 300;

  const margin = { top: 20, right: 10, left: 25, bottom: 20};


  $: innerWidth = width - margin.left - margin.right;
  let innerHeight = height - margin.top - margin.bottom;


  const continents = ["Oceania", "Asia", "Africa", "Americas", "Europe", ]

  console.log(continents)

  $: xScale = scaleLinear()
    .domain([1947, max(data, d => d.entered)])
    .range([0, innerWidth]);
  
  let yScale = scaleLinear()
    .domain([0, 30])
    .range([innerHeight, 0]);

  //color of circles
  const colorRange = ["#0043ef", "#ef7f31", "#a732d0", "#3ab091", "#d74e45"];
  const colorScale  = scaleOrdinal()
    .domain(continents)
    .range(colorRange);


  //tooltip

  let hovered, hoveredContinent;

</script>

<div class="chart">
<h1>Rise of foreign players in the NBA</h1>
<h2>Players from outside the US entering the NBA by year</h2>
<Legend {colorScale} bind:hoveredContinent/>
<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class='chart-container'
     bind:clientWidth={width}
     on:click={() => {
      hovered=null;
     }}
     on:mouseleave={() => hovered = null}
     >
  <svg {width} {height}>
    <g class="inner-chart" transform="translate({margin.left}, {margin.top})">
      <AxisX xScale={xScale} width={innerWidth} height={innerHeight}/>
      <AxisY yScale={yScale} width={innerWidth}/>
    {#each data as d}
      <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
      <circle
        cx={xScale(d.entered)}
        cy={yScale(d.rank)}
        r={width < 550 ? 3.5 : 3.75}
        fill={colorScale(d.continent)}
        stroke="white"
        opacity={hovered || hoveredContinent ? hovered === d || hoveredContinent === d.continent ? 1 :0.3 : 1 }
        stroke-width="0.2"
        on:mouseover={() => (hovered = d)}
        on:focus={() => (hovered = d)}
        tabindex="0"
        
      />
    {/each}
    </g>
  </svg>
</div>
<p>
  Hover to view player information.
</p>
</div>
{#if hovered}
  <Tooltip data={hovered} {colorScale} {xScale} {yScale} {width}/>
{/if}
<style>

  .chart {
    background-color: rgb(38,38,38);
  }

  :global(.tick text) {
    font-weight: 100; /* How thick our text is */
    font-size: 12px; /* How big our text is */
    fill: whitesmoke;
  }

  h1 {
    font-size: 20px;
    color: whitesmoke;
    font-weight: 400;
    margin-bottom: 5px;
  }

  h2, p {
    font-size: 16px;
    color: whitesmoke;
    font-weight: 300;
    margin-bottom: 15px;
  }
</style>