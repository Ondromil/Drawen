<script lang="ts">
    import { onMount } from "svelte";
    import {fly} from "svelte/transition";

    export let colorHexValue =  '#000000';
    export let brushSize = 4;
    export let navVisible = true;
    
    let canvasWidth = 1200;
    let canvasHeight = 600;
    let canvas: HTMLCanvasElement;
    let ctx: CanvasRenderingContext2D;
    let isDrawing: Boolean;
    let buffer: HTMLCanvasElement;
    let bufferCtx: CanvasRenderingContext2D;

    let dimensionsInputVisible = false;
    let inputXValue = 1200;
    let inputYValue = 600;

    onMount(() => {
       ctx = canvas.getContext('2d');
       bufferCtx = buffer.getContext('2d');
       ctx.imageSmoothingEnabled = true;
       ctx.fillStyle = 'white'
       ctx.fillRect(0, 0, canvas.width, canvas.height)
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

    const handleDimensionsButtonClick = () => {
        if(dimensionsInputVisible) {
            dimensionsInputVisible = false
        }
        else {
            dimensionsInputVisible = true
        }
    }

    const changeXDimension = () => {
        bufferCtx.drawImage(canvas, 0, 0);
        canvas.width = inputXValue
        ctx.fillStyle = 'white'
        ctx.fillRect(0, 0, canvas.width, canvas.height)
        ctx.drawImage(buffer, 0, 0);
    }

    const changeYDimension = () => {
        bufferCtx.drawImage(canvas, 0, 0);
        canvas.height = inputYValue
        ctx.fillStyle = 'white'
        ctx.fillRect(0, 0, canvas.width, canvas.height)
        ctx.drawImage(buffer, 0, 0);
    }

    const hideNav = () => {
        if(navVisible) {
          navVisible = false
        }
        else { 
           navVisible = true
        }
    }
</script>

{#if navVisible}
<div class="h-[110px] w-full" in:fly|local="{{ y: -100, duration: 500 }}"></div>
{/if}
<div class="w-full h-full bg-slate-500 relative">
    <div class="top-32 left-6 fixed z-20 ">
        <ul>
            <li><button class="side-button btn btn-ghost" on:click={saveCanvas}><img src="src\lib\Icons\icons8-save-50.png" alt="Save project icon"></button></li>
            <li><button class="side-button btn btn-ghost" on:click={clearCanvas}><img src="src\lib\Icons\icons8-trash-bin-78.png" alt="Clear canvas icon"></button></li>
            <li><button class="side-button btn btn-ghost" on:click={hideNav}><img src="src\lib\Icons\icons8-hide-64.png" alt="Hide navbar icon"></button></li>
            <li class="flex items-center gap-2">
                <button class="side-button btn" on:click={handleDimensionsButtonClick}><img src="src\lib\Icons\icons8-surface-50.png" alt="Clear canvas icon"></button>
                {#if dimensionsInputVisible}
                   <div class="block">
                       <label class="input-group input-group-xs my-[2px]">
                          <span>X</span>
                          <input type="text" placeholder="Type" maxlength="4" class="input input-xs" bind:value={inputXValue} on:change={changeXDimension}/>
                       </label>
                       <label class="input-group input-group-xs my-[2px]">
                          <span>Y</span>
                          <input type="text" placeholder="Type" maxlength="4" class="input input-xs" bind:value={inputYValue} on:change={changeYDimension}/>
                     </label>        
                   </div>
                {/if}
            </li>  
        </ul>
    </div>
    <canvas 
     class="m-auto z-10" 
     width={canvasWidth}
     height={canvasHeight}
     bind:this={canvas}
     on:mousedown={handleStart}
     on:mousemove={handleMove}
     on:mouseup={handleEnd}
     on:mouseleave={handleEnd}
     on:click={() => dimensionsInputVisible = false}
    ></canvas>  
</div>

<canvas                      
   bind:this={buffer}
   width={canvasHeight} 
   height={canvasWidth}
   class="hidden"
></canvas>

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
    input {
        background-color: #2A303C;
        color: #A6ADBB;
        width: 50px;
        height: 20px;
        display: block;
    }
    span {
        background-color: rgb(42, 41, 41);
        color: #A6ADBB;
    }
</style>