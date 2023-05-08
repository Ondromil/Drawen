<script lang="ts">
    import { onMount } from "svelte";

    export let colorHexValue =  '#000000';
    export let brushSize = 4;
    
    let canvasWidth = 1200;
    let canvasHeight = 600;
    let canvas: HTMLCanvasElement;
    let ctx: CanvasRenderingContext2D;
    let isDrawing: Boolean;

    onMount(() => {
       ctx = canvas.getContext('2d');
       ctx.imageSmoothingEnabled = true;
       ctx.fillStyle = 'white'
       ctx.fillRect(0, 0, canvasWidth, canvasHeight)
    })

    $: if(ctx) {
        ctx.strokeStyle = colorHexValue;
        ctx.lineWidth = brushSize;
    }

    const handleStart = ({offsetX: x, offsetY: y}) => {
        isDrawing = true;
        ctx.lineCap = 'round'
        ctx.lineTo(x, y)
        ctx.stroke()
        ctx.beginPath()
        ctx.moveTo(x, y)
    }

    const handleMove = ({offsetX: x, offsetY: y}) => {
        if (isDrawing) {
            ctx.lineCap = 'round'
            ctx.lineTo(x, y)
            ctx.stroke()
            ctx.beginPath()
            ctx.moveTo(x, y)
        } 
    }

    const handleEnd = () => {
        ctx.beginPath()
        isDrawing = false;
    }

    const saveCanvas = () => {
        const dataUrl = canvas.toDataURL('image/jpeg');
        const link = document.createElement('a');
        link.download = 'untitled-canvas.jpg'
        link.href = dataUrl;
        link.click();
    }

    const clearCanvas =() => {
        ctx.clearRect(0, 0, canvasWidth, canvasHeight)
        ctx.fillRect(0, 0, canvasWidth, canvasHeight)
    }
</script>

<div class="w-full h-full bg-slate-500 flex relative">
    <div class="absolute inset-3">
        <ul>
            <li><button class="side-button btn" on:click={saveCanvas}><img src="src\lib\Icons\icons8-save-50.png" alt="Save project icon"></button></li>
            <li><button class="side-button btn" on:click={clearCanvas}><img src="src\lib\Icons\icons8-trash-bin-78.png" alt="Clear canvas icon"></button></li> 
        </ul>
    </div>
    <canvas 
     class="m-auto z-20" 
     width={canvasWidth}
     height={canvasHeight}
     bind:this={canvas}
     on:mousedown={handleStart}
     on:mousemove={handleMove}
     on:mouseup={handleEnd}
     on:mouseleave={handleEnd}
    ></canvas>  
</div>

<style>
    .side-button {
        background-color: rgb(42, 48, 60);
        color: rgb(166, 173, 187);
        border-radius: 50%;
        width: 55px;
        height: 55px;
        margin: 5px 0;
    }
    .side-button:hover {
        opacity: 0.6;
    }
</style>