<script lang="ts">
    import { foot, houseRadius, width } from "./consts";

    export let x;
    export let y;
    export let fill;

    let moving = false;

    const start = () => {
        moving = !moving;
    }

    const move = (e) => {
        if (moving) {
            x += e.movementX;
            y += e.movementY;
        }
    }

    const onKeyDown = (e) => {
        if (moving) {
            if (e.key == "c") {
                stop();
                x = width / 2;
            } else if (e.key == "t") {
                stop();
                y = houseRadius;
            } else if (e.key == "b") {
                stop();
                x = width / 2;
                y = houseRadius;
            }
        }
    }

    const stop = () => {
        moving = false;
    }
</script>

<svelte:window on:mousemove={move} on:keydown={onKeyDown} />
<div
        on:mousedown={start}
        style={`width: ${foot-8}px; height: ${foot-8}px; background-color: ${fill}; left: ${x}px; top: ${y}px`}
>
</div>

<style>
    div {
        border-radius: 50%;
        position: absolute;
        border: 4px solid grey;
        outline: 2px solid black;
        transform: translate(-50%, -50%);
    }
</style>
