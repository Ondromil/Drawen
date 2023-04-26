<script lang="ts">
	import Canvas from "$lib/components/Canvas.svelte"
	import Nav from "$lib/components/Nav.svelte";

	let colorHexValue: string;
	let brushSize: number;
</script>

<main>
     <Nav 
	    bind:colorHexValue
		bind:brushSize
	  />
     <Canvas 
	    {colorHexValue} 
		{brushSize}
	  /> 
</main>