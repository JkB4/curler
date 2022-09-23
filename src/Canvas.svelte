<script lang="ts">
    import { onMount, setContext } from "svelte";
    import { width, height } from "./consts";

    let canvas;

    const drawFunctions = [];

    setContext("canvas", {
        register(drawFn) {
            drawFunctions.push(drawFn);
        },
        unregister(drawFn) {
            drawFunctions.splice(drawFunctions.indexOf(drawFn), 1);
        }
    });

    onMount(() => {
        const ctx = canvas.getContext("2d");

        const update = () => {
            ctx.clearRect(0, 0, width, height);
            drawFunctions.forEach(drawFn => {
                drawFn(ctx);
            })

            frameId = requestAnimationFrame(update);
        }

        let frameId = requestAnimationFrame(update);

        return () => {
            cancelAnimationFrame(update);
        }
    });
</script>

<canvas
    bind:this={canvas}
    width={width}
    height={height}
>
    <slot />
</canvas>

<style>
    canvas {
        background-color: #f9f9f9;
        outline: 4px solid black;
    }
</style>