<script lang="ts">
	import Canvas from "$lib/components/Canvas.svelte"
	import Nav from "$lib/components/Nav.svelte";

	const colors = [
		'#000000',
		'#FFFFFF',
		'#FACC15'
	]

	let brushColor = colors[0];
</script>

<Nav/>
<Canvas {brushColor}/> 
