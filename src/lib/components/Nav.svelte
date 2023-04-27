<script>
    export let colorHexValue;
    export let brushSize;

    let sliderValue = 4;

    function changeBrushColor(colorIndex) {
        colorHexValue = colors[colorIndex];
    }

    function changeBrushSize() {
        brushSize = sliderValue;
    }

    const colors = [
	     '#000000',
	     '#FFFFFF',
	     '#FACC15',
       '#2563EB',
       '#DC2626',
       '#22C55E',
       '#94A3B8',
       '#FB923C',
       '#9333EA',
       '#B75309',
       '#A3E635',
       '#60A5FA',
       '#F472B6',
       '#166534',
       '#2DD4BF',
       '#4F46E5'
      ]
</script>

<nav class="navbar bg-base-100">
   <div class="flex-none">
    <div class="dropdown">
       <button class="btn btn-square btn-ghost">
         <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-5 h-5 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path></svg>
       </button>
       <ul class="menu dropdown-content mt-5 bg-base-100 rounded-xl w-40 text-[1.3em]">
          <li><button on:click={null}>Save Project</button></li>
          <li><button on:click={null}>Clear</button></li>
          <li><a href="/about">About</a></li>
       </ul>
     </div>
    </div>
    <div class="flex-1">
       <p class="text-2xl ml-4">Drawen.io</p>
    </div>
    <div class="mr-8 block text-center">
      <p>Brush size</p>
      <input type="range" min=1 max=100 class="range range-xs" bind:value={sliderValue} on:change={changeBrushSize}/> 
    </div>
    <div class="">
      <svg height="60" width="60">
        <circle cx="20" cy="28" r="18" fill={colorHexValue} />
      </svg>
    </div>
    <div class="block mr-6">
      <ul class="flex gap-1.5">
        {#each Array(8) as _, i}
           <li><button style="background-color: {colors[i]};" class="btn btn-square btn-sm rounded-md" on:click={() => changeBrushColor(i)}></button></li>
        {/each}
      </ul>
      <ul class="flex gap-1.5">
        {#each Array(8) as _, i}
           <li><button style="background-color: {colors[i + 8]};" class="btn btn-square btn-sm rounded-md" on:click={() => changeBrushColor(i + 8)}></button></li>
        {/each}
      </ul>
    </div>
    <div class="mr-4">
       <button class="btn btn-circle btn-ghost w-20">
          Change color
       </button>
    </div>
</nav>