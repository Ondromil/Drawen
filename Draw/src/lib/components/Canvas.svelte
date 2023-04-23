<script lang="ts">
    import { onMount } from "svelte";

    let canvas: HTMLCanvasElement;
    let ctx: CanvasRenderingContext2D;
    let isDrawing: Boolean;
    let start;
    export let brushColor = '#000000';
  
    onMount(() => {
       ctx = canvas.getContext('2d');
       ctx.lineWidth = 4;
       ctx.globalAlpha = 2000;
    })

    $: if(ctx) {
        ctx.strokeStyle = brushColor;
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

    export function saveCanvas() {
        const dataUrl = canvas.toDataURL('image/jpeg');
        const link = document.createElement('a');
        link.download = 'canvas.jpg'
        link.href = dataUrl;
        link.click();
    }
</script>

<div class="w-full h-screen bg-slate-500">
    <canvas 
     class="bg-white m-auto" 
     width="1200"
     height="600"
     bind:this={canvas}
     on:mousedown={handleStart}
     on:mousemove={handleMove}
     on:mouseup={handleEnd}
     on:mouseleave={handleEnd}
    ></canvas>   
</div>





