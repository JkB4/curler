<script lang="ts">
    import { getContext, onMount } from "svelte";
    import { foot } from "./consts";

    export let cx;
    export let cy;
    export let fill;

    const { register, unregister } = getContext("canvas");

    onMount(() => {
        register(draw);

        return () => {
            unregister(draw);
        }
    });

    const draw = (ctx) => {
        ctx.beginPath();
        ctx.lineWidth = 2;
        ctx.arc(cx, cy, foot / 2, 0, 2 * Math.PI, false);
        ctx.fillStyle = fill;
        ctx.fill();
        ctx.strokeStyle = "#000";
        ctx.stroke();
    }
</script>