<svelte:head>
	<title>About</title>
</svelte:head>

<div class="bg-[#1D1D1D] h-screen w-screen absolute z-10">
	<div class="w-[75vw] m-auto mt-20">
		<div>
			<article>
				<header>
					<h1 class="text-3xl"><strong>About</strong></h1>
				</header>
				<section class="mt-6">
					<p>
						Drawen is a canvas drawing application currently in development. <br /> As of right now,
						it includes custom color palette, brush size slider and options to save, clear and resize
						canvas.
					</p>
				</section>
			</article>
		</div>
		<div class="text-center mt-[280px]">
			<button><a href="/">Return</a></button>
		</div>
	</div>
</div>

<footer class="w-screen h-12 bg-[#3d3d3d] z-20 absolute bottom-0">
	<div class="text-center text-lg mt-2">
		<p>Made by Ondřej Hlaváč @2023</p>
	</div>
</footer>

<style>
	p, a, h1 {
		color: #a6adbb;
	}
	button a {
		padding: 15px 60px;
		font-size: 2.5em;
		background-color: #5a5a5a;
		border-radius: 40px;
		font-weight: 600;
	}
	button:hover {
		filter: brightness(120%);
		-webkit-filter: brightness(120%);
	}
</style>
