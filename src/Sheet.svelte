<script lang="ts">
    import { getContext, onMount } from "svelte";

    export let c1;
    export let c2;

    const width = 500;
    const height = 823;
    const houseRadius = width * 0.7316 / 2;

    const { register, unregister } = getContext("canvas");

    const drawRing = (ctx, num, clr) => {
        ctx.beginPath();
        ctx.lineWidth = 2;
        ctx.arc(width / 2, houseRadius, houseRadius * num / 12, 0, 2 * Math.PI, false);
        ctx.fillStyle = clr;
        ctx.fill();
        ctx.strokeStyle = "#000";
        ctx.stroke();
    };

    const drawLine = (ctx, x, y, w, h) => {
        ctx.beginPath();
        ctx.lineWidth = 2;
        ctx.moveTo(x, y);
        ctx.lineTo(w, h);
        ctx.stroke();
    };

    onMount(() => {
        register(draw);

        return () => {
            unregister(draw);
        }
    });

    const draw = (ctx) => {
        drawRing(ctx, 12, c1);
        drawRing(ctx, 8, "white");
        drawRing(ctx, 4, c2);
        drawLine(ctx, width / 2, 0 , width / 2, height);
        drawLine(ctx, 0, houseRadius, width, houseRadius);
        drawRing(ctx, 1, "white");
        drawRing(ctx, 0.05, "black");
    }
</script>