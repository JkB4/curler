<script lang="ts">
    import Canvas from "./Canvas.svelte";
    import Rock from "./Rock.svelte";
    import Sheet from "./Sheet.svelte";
    import { foot, height, width } from "./consts";

    let rocks = [];

    for (let i = 0; i < 16; i++) {
        let fill = i < 8 ? "red" : "yellow";
        let x = i < 8 ? -foot : width + foot;
        let y = height - foot / 2 - foot * 1.25 * (i < 8 ? i : i - 8)

        rocks.push({ x: x, y: y, fill: fill });
    }

    console.log(rocks);

    let x = 200;
    let y = 200;
</script>

<main>
    <div class="sheet">
        <Canvas>
            <Sheet c1="green" c2="blue" />
        </Canvas>

        {#each rocks as rock, i}
            <Rock x={rock.x} y={rock.y} fill={rock.fill}/>
        {/each}
    </div>

</main>

<style>
    :root {
        background-color: #1a1a1a;
    }
    
    .sheet {
        position: relative;
    }
</style>