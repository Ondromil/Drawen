<script lang="ts">
	import Canvas from "$lib/components/Canvas.svelte"
	import Nav from "$lib/components/Nav.svelte";

	let colorHexValue: string;
	let brushSize: number;
	let navVisible: boolean;
</script>

<svelte:head>
    <title>Drawen</title>
</svelte:head>

<main>
    <Nav 
	   bind:colorHexValue
	   bind:brushSize
       {navVisible}
	/>
   <Canvas 
       bind:navVisible
	   {colorHexValue} 
	   {brushSize}
    /> 
</main>