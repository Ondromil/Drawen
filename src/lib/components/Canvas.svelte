<script lang="ts">
    import { onMount } from "svelte";

    export let colorHexValue =  '#000000';
    export let brushSize = 4;
    
    let canvasWidth = 1200;
    let canvasHeight = 600;
    let canvas: HTMLCanvasElement;
    let ctx: CanvasRenderingContext2D;
    let isDrawing: Boolean;
    let start;

    onMount(() => {
       ctx = canvas.getContext('2d');
       ctx.imageSmoothingEnabled = true;
    })

    $: if(ctx) {
        ctx.strokeStyle = colorHexValue;
        ctx.lineWidth = brushSize;
    }

    const handleStart = ({offsetX: x, offsetY: y}) => {
        isDrawing = true;
        start = {x, y};
    }

    const handleMove = ({offsetX: x1, offsetY: y1}) => {
        if (isDrawing) {
            ctx.beginPath()
            ctx.moveTo(start.x, start.y)
            ctx.lineTo(x1, y1)
            ctx.closePath()
            ctx.stroke()
            
            start = {x: x1, y: y1}
        } 
    }

    const handleEnd = () => {
        isDrawing = false;
    }

    export const saveCanvas = () => {
        const dataUrl = canvas.toDataURL('image/jpeg');
        const link = document.createElement('a');
        link.download = 'canvas.jpg'
        link.href = dataUrl;
        link.click();
    }

    export const clearCanvas =() => {
        ctx.clearRect(0, 0, canvasWidth, canvasHeight)
    }
</script>

<div class="w-full h-screen bg-slate-500">
    <canvas 
     class="bg-white m-auto" 
     width={canvasWidth}
     height={canvasHeight}
     bind:this={canvas}
     on:mousedown={handleStart}
     on:mousemove={handleMove}
     on:mouseup={handleEnd}
     on:mouseleave={handleEnd}
    ></canvas>   
    <button on:click={saveCanvas}>Save</button>
</div>