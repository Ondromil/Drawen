<script lang="ts">
	import Canvas from "$lib/components/Canvas.svelte"
	import Nav from "$lib/components/Nav.svelte";

	let brushIndex: number;
	let brushSize: number;
</script>

<main>
     <Nav 
	    bind:index={brushIndex}
		bind:rangeValue={brushSize}
	  />
     <Canvas 
	    {brushIndex} 
		{brushSize}
	  /> 
</main>