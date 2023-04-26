<script lang="ts">
    import { onMount } from "svelte";

    let canvas: HTMLCanvasElement;
    let ctx: CanvasRenderingContext2D;
    let isDrawing: Boolean;
    let start;
    export let brushIndex = 0;
    export let brushSize = 4;

	const colors = [
	   '#000000',
	   '#FFFFFF',
	   '#FACC15',
       '#2563EB',
       '#DC2626',
       '#22C55E',
       '#94A3B8',
       '#FB923C',
       '#9333EA',
       '#B75309',
       '#A3E635',
       '#60A5FA',
       '#F472B6',
       '#166534',
       '#2DD4BF',
       '#4F46E5'
	]
  
    onMount(() => {
       ctx = canvas.getContext('2d');
       ctx.imageSmoothingEnabled = true;
    })

    $: if(ctx) {
        ctx.strokeStyle = colors[brushIndex];
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
    <button on:click={saveCanvas}>Save</button>
</div>