<script lang="ts">
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';

	export let colorHexValue = '#000000';
	export let brushSize = 4;
	export let opacity = 1;
	export let navVisible = true;
	export let bucketOn = false;
	export let eraserOn = false;

	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D;
	let isDrawing: Boolean;
	let leftMouseDown = false;
	let buffer: HTMLCanvasElement;
	let bufferCtx: CanvasRenderingContext2D;
	let bufferCanvasWidth = 1400;
	let bufferCanvasHeight = 800;

	let undoCanvas: HTMLCanvasElement;
	let undoCanvasCtx: CanvasRenderingContext2D;
	let undoCanvasWidth = 1400;
	let undoCanvasHeight = 800;
	let lastUndoCanvas: HTMLCanvasElement;
	let nextRedoCanvas: HTMLCanvasElement;

	let dimensionsInputVisible = false;
	let inputXValue = 1400;
	let inputYValue = 800;

	let undoCanvases = [];
	let redoCanvases = [];

	let windowWidth;

	onMount(() => {
		ctx = canvas.getContext('2d');
		bufferCtx = buffer.getContext('2d');
		undoCanvasCtx = undoCanvas.getContext('2d');
		ctx.imageSmoothingEnabled = true; // Anti-aliasing
		ctx.fillStyle = 'white';
		ctx.fillRect(0, 0, canvas.width, canvas.height); // Draws white rectangle over canvas, because default canvas color after saving is black
	});

	$: if (ctx) {
		if (eraserOn) {
			ctx.strokeStyle = "#FFFFFF"
			ctx.globalAlpha = 100;
		} else {
		    ctx.strokeStyle = colorHexValue;
			ctx.globalAlpha = opacity / 100;
		}
		ctx.lineWidth = brushSize;
	}

	const handleStart = ({ offsetX: x, offsetY: y }) => {
		undoCanvasWidth = canvas.width;
		undoCanvasHeight = canvas.height;
		undoCanvas = document.createElement('canvas');
		undoCanvas.width = undoCanvasWidth;
		undoCanvas.height = undoCanvasHeight;
		undoCanvasCtx = undoCanvas.getContext('2d');
		undoCanvasCtx.drawImage(canvas, 0, 0);
		undoCanvases.push(undoCanvas);
		redoCanvases = [];

		isDrawing = true;
		if (!bucketOn) {
	    	ctx.lineCap = 'round';
	        ctx.lineTo(x, y);
		    ctx.stroke();
		    ctx.beginPath();
	     	ctx.moveTo(x, y);
		} else {
			ctx.fillStyle = colorHexValue;
			ctx.fillRect(0, 0, canvas.width, canvas.height);
		} 

	};

	const handleMove = ({ offsetX: x, offsetY: y }) => {
		// Draws line made of circles
		if (isDrawing && leftMouseDown && !bucketOn) {
			ctx.lineCap = 'round';
			ctx.lineTo(x, y);
			ctx.stroke();
			ctx.beginPath();
			ctx.moveTo(x, y);
		}
	};

	const handleEnd = () => {
		ctx.stroke();
		ctx.beginPath();
	};

	const globalMouseDown = () => {
		leftMouseDown = true;
	}

	const globalMouseUp = () => {
		leftMouseDown = false;
	}

	const saveCanvas = () => {
		const dataUrl = canvas.toDataURL('image/jpeg');
		const link = document.createElement('a');
		link.download = 'untitled-canvas.jpg';
		link.href = dataUrl;
		link.click();
	};

	const clearCanvas = () => {
		ctx.clearRect(0, 0, canvas.width, canvas.height);
		ctx.globalAlpha = 1;
		ctx.fillRect(0, 0, canvas.width, canvas.height);
		ctx.globalAlpha = opacity / 100;
	};

	const handleDimensionsButtonClick = () => {
		if (dimensionsInputVisible) {
			dimensionsInputVisible = false;
		} else {
			dimensionsInputVisible = true;
		}
	};

	const changeXDimension = () => {
		if (inputXValue != null && inputXValue >= 1) {
			// Canvas pernamently dissapears if value is below 1, null or not a number
			bufferCtx.drawImage(canvas, 0, 0);
			canvas.width = inputXValue;
			bufferCanvasWidth = inputXValue;
			ctx.fillStyle = 'white';
			ctx.fillRect(0, 0, canvas.width, canvas.height);
			ctx.drawImage(buffer, 0, 0);
		}
	};

	const changeYDimension = () => {
		if (inputYValue != null && inputYValue >= 1) {
			bufferCtx.drawImage(canvas, 0, 0);
			canvas.height = inputYValue;
			bufferCanvasHeight = inputYValue;
			ctx.fillStyle = 'white';
			ctx.fillRect(0, 0, canvas.width, canvas.height);
			ctx.drawImage(buffer, 0, 0);
		}
	};

	const handleUndo = () => {
		if (undoCanvases.length > 0) {
	    	lastUndoCanvas = undoCanvases.pop()
			redoCanvases.unshift(lastUndoCanvas);
			console.log(redoCanvases)
	    	ctx.drawImage(lastUndoCanvas, 0, 0);
		}
	}

	const handleRedo = () => {
		if (redoCanvases.length > 0) {
	     	undoCanvases.push(redoCanvases[0]);
	    	nextRedoCanvas = redoCanvases.shift();
			console.log(undoCanvases)
	    	ctx.drawImage(nextRedoCanvas, 0, 0);
		}
	}

	const hideNav = () => {
		if (navVisible) {
			navVisible = false;
		} else {
			navVisible = true;
		}
	};

</script>

<svelte:window bind:innerWidth={windowWidth} />

{#if navVisible}
	<div class="h-[110px] w-full" in:fly|local={{ y: -100, duration: 500 }} />
{/if}
<div class="w-full h-full bg-slate-500 relative">
	<div class="top-32 left-6 fixed z-20">
		<ul>
			<li>
				<button class="side-button btn btn-ghost" on:click={saveCanvas}
					><img src="/icons8-save-50.png" alt="Save project icon" /></button
				>
			</li>
			<li>
				<button class="side-button btn btn-ghost" on:click={handleUndo}
					><img src="/iconundo.svg" alt="undo-button" /></button
				>
			</li>
			<li>
				<button class="side-button btn btn-ghost" on:click={handleRedo}
					><img src="/iconredo.svg" alt="redo-button" /></button
				>
			</li>
			<li class="flex items-center gap-2">
				<button class="side-button btn" on:click={handleDimensionsButtonClick}
					><img src="/icons8-surface-50.png" alt="Clear canvas icon" /></button
				>
				{#if dimensionsInputVisible}
					<div class="block">
						<label class="input-group input-group-xs my-[2px]">
							<span>X</span>
							<input
								type="text"
								placeholder="Type"
								maxlength="4"
								class="input input-xs"
								bind:value={inputXValue}
								on:change={changeXDimension}
							/>
						</label>
						<label class="input-group input-group-xs my-[2px]">
							<span>Y</span>
							<input
								type="text"
								placeholder="Type"
								maxlength="4"
								class="input input-xs"
								bind:value={inputYValue}
								on:change={changeYDimension}
							/>
						</label>
					</div>
				{/if}
			</li>
			<li>
				<button class="side-button btn btn-ghost" on:click={hideNav}
					><img src="/icons8-hide-64.png" alt="Hide navbar icon" /></button
				>
			</li>
			<li>
				<button class="side-button btn btn-ghost" on:click={clearCanvas}
					><img src="/icons8-trash-bin-78.png" alt="Clear canvas icon" /></button
				>
			</li>
		</ul>
	</div>

	<canvas
	class="m-auto z-20"
	width="1400"
	height="800"
	bind:this={canvas}
	on:mousedown={handleStart}
	on:mousemove={handleMove}
	on:mouseup={handleEnd}
	on:mouseleave={handleEnd}
	on:touchstart|preventDefault={handleStart}
	on:touchmove|preventDefault={handleMove}
	on:click={() => (dimensionsInputVisible = false)}
    /> 
</div>


<!-- Buffer canvas where current drawing is saved before resizing -->
<canvas bind:this={buffer} width={bufferCanvasWidth} height={bufferCanvasHeight} class="hidden" />

<canvas bind:this={undoCanvas} width={undoCanvasWidth} height={undoCanvasHeight} class="hidden"/>

<svelte:body
	on:mousedown={globalMouseDown}
	on:mouseup={globalMouseUp}
	on:mouseleave={globalMouseUp}
/>

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
		background-color: #2a303c;
		color: #a6adbb;
		width: 50px;
		height: 20px;
		display: block;
	}
	input:focus {
		outline: none;
	}
	input::-webkit-outer-spin-button,
	input::-webkit-inner-spin-button {
		-webkit-appearance: none;
	}
	span {
		background-color: rgb(42, 41, 41);
		color: #a6adbb;
	}
</style>
