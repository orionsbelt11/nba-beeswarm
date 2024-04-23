<script>
    export let data;

    const x = 200;
    const y = 150;
</script>

<div class="annotate"
     style="left:{x}px; top: {y}px;">
    <span>
        <p>hello</p>
    </span>
</div>

<style>
    .annotate {
        position: absolute;
        padding: 8px 6px;
        background-color: aliceblue;
        box-shadow: rgba(0, 0, 0, 0.15) 2px 3px 8px;
        border-radius: 4px;
        min-width: 100px;
        pointer-events: none;
        transition: top 300ms ease, left 300ms ease;
    }
</style>