<script>
    import { reverse } from "d3-array";
    export let colorScale;
    export let hoveredContinent;
</script>

<div class="legend" on:mouseleave={() => (hoveredContinent = null)}>
    {#each colorScale.domain().reverse() as continent}
        <!-- svelte-ignore a11y-mouse-events-have-key-events -->
        <p class:unhovered={hoveredContinent && hoveredContinent !== continent} 
        on:mouseover={() => (hoveredContinent = continent)}> 
            <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
            <span 
                style="background: {colorScale(continent)}"/>
            {continent}
        </p>
    {/each}
</div>

<style>
    .legend {
        display: flex;
        place-items: center;
        justify-content: center;
        flex-direction: row;
        flex-wrap: wrap;
        column-gap: 10px;
        row-gap: 5px;
        margin-top: 0.5rem;
        margin-bottom: 0.5rem;
    }

    p {
        color: white;
        margin: 0;
        cursor: pointer;
    }

    p.unhovered {
        opacity: 0.3;
    }

    span {
        width: 9px;
        height: 9px;
        display: inline-block;
        border-radius: 50%;
        border: 1px solid rgba(235, 232, 232, 0.5);
    }
</style>