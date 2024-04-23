<script>
    import {fly, fade } from "svelte/transition";
    export let data;
    export let colorScale;
    export let xScale;
    export let yScale;
    export let width;

    $: x = xScale(data.entered)
    $: y = yScale(data.rank)

    let tooltipWidth;

    const xNudge = 40;
    const yNudge = 5;

    $: xPosition = x + tooltipWidth > width ? x - tooltipWidth - xNudge: x + xNudge;
    $: yPosition = y + yNudge;

console.log(tooltipWidth)
</script>

<div class="tooltip"
     in:fly={{ y: 10, duration: 200, delay: 200}}
     out:fade
     style="left:{xPosition}px; top:{yPosition}px;"
     bind:clientWidth={tooltipWidth}>

    <h1>
        {data.player} <span style="background: {colorScale(data.continent)}; border-radius: 5px;">{data.continent}</span>
    </h1>

    <p>
        Career points: {data.pts}
    </p>
    <p>
        Country: {data.country} 
    </p>
    <p>
        Entered NBA: {data.entered}
    </p>
</div>

<style>
    .tooltip {
        position: absolute;
        padding: 8px 6px;
        background-color: aliceblue;
        box-shadow: rgba(0, 0, 0, 0.15) 2px 3px 8px;
        border-radius: 4px;
        min-width: 150px;
        pointer-events: none;
        transition: top 300ms ease, left 300ms ease;
    }

    h1 {
        font-size: 1rem;
        font-weight: 600;
        margin-bottom: 6px;
        width: 100%;
    }
</style>