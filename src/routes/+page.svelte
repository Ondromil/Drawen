<script lang="ts">
	import Canvas from '$lib/components/Canvas.svelte';
	import Nav from '$lib/components/Nav.svelte';

	let colorHexValue: string;
	let brushSize: number;
	let opacity: number;
	let navVisible: boolean;
	let bucketOn: boolean;
	let eraserOn: boolean;
</script>

<svelte:head>
	<title>Drawen</title>
</svelte:head>

<main>
	<Nav bind:colorHexValue bind:brushSize bind:opacity bind:bucketOn bind:eraserOn {navVisible} />
	<Canvas bind:navVisible {colorHexValue} {brushSize} {opacity} {bucketOn} {eraserOn} />
</main>
