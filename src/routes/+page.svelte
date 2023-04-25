<script lang="ts">
	import Canvas from "$lib/components/Canvas.svelte"
	import Nav from "$lib/components/Nav.svelte";

	let brushIndex: number;
</script>

<main>
     <Nav bind:index={brushIndex}/>
     <Canvas {brushIndex}/> 
</main>