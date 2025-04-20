<script lang="ts">
   import {fly} from "svelte/transition";

   export let colorHexValue: string;
   export let brushSize = 4;
   export let opacity = 100;
   export let navVisible = true;

   let sliderValue = 4;
   let opacitySliderValue = 100;
   let changeButtonText = 'Change Color';
   let changingColor;
   let inputHex = '#';
   let visible = false;
   let ColorIndex;

   function handleColorButtonClick(colorIndex) {
      if (changingColor) {
         visible = true
         ColorIndex = colorIndex
      }
      else {
         colorHexValue = colors[colorIndex];
      }
    }

   function changeBrushSize() {
      brushSize = sliderValue;
   }

   function changeOpacity() {
      opacity = opacitySliderValue;
   }

   function handleChangeButtonClick() {
      if (changingColor) {
         changingColor = false;
         visible = false;
         changeButtonText = 'Change Color'
      }
      else {
         changeButtonText = 'Select or cancel'
         changingColor = true
      }
    }

   function endChange() {
       colors[ColorIndex] = inputHex;
       visible = false;
       changingColor = false
       changeButtonText = 'Change Color'
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

{#if navVisible}
   <nav class="navbar z-40 h-[110px] bg-[#2A303C] text-[#A6ADBB] fixed" in:fly|local="{{ y: -100, duration: 500 }}" out:fly|local="{{ y: -100, duration: 500 }}">
      <div class="dropdown">
         <button class="btn btn-square btn-ghost">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-5 h-5 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path></svg>
         </button>
         <ul class="menu dropdown-content mt-5 rounded-xl w-40 text-[1.3em] bg-[#2A303C]">
             <li><a href="/about">About</a></li>
         </ul>
      </div>
      <div class="flex-1">
         <p class="text-3xl ml-4">Drawen.io</p>
      </div>
      <div class="block mr-6">
         <div class="flex flex-col">
             <button class="btn btn-ghost btn-md"><img src="/bucket.svg" alt="bucket-button" width="32" height="32" /></button>
             <button class="btn btn-ghost btn-md"><img src="/eraser-fill.svg" alt="eraser-button" width="32" height="32"/></button>
         </div>
      </div>
      <div class="block">
         <div class="mr-8 block text-center">
           <p>Brush size - {brushSize} px</p>
           <input type="range" min=1 max=200 class="nav-range" bind:value={sliderValue} on:input={changeBrushSize}/> 
         </div>
         <div class="mr-8 block text-center">
           <p>Opacity - {opacity} %</p>
           <input type="range" min=1 max=100 class="nav-range" bind:value={opacitySliderValue} on:input={changeOpacity}/> 
         </div>
      </div>
      <div class="mr-6">
         <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill={colorHexValue} version="1.1" id="Capa_1" width="50px" height="50px" viewBox="0 0 264.564 264.564" xml:space="preserve">
            <g>
               <g>
                  <path d="M132.281,264.564c51.24,0,92.931-41.681,92.931-92.918c0-50.18-87.094-164.069-90.803-168.891L132.281,0l-2.128,2.773    c-3.704,4.813-90.802,118.71-90.802,168.882C39.352,222.883,81.042,264.564,132.281,264.564z"/>
               </g>
            </g>
        </svg>
      </div>
      <div class="block mr-2">
         <ul class="flex gap-1.5">
           {#each Array(8) as _, i}
              <li><button style="background-color: {colors[i]};" class="btn btn-square btn-sm rounded-md" on:click={() => handleColorButtonClick(i)}></button></li>
           {/each}
         </ul>
         <ul class="flex gap-1.5">
           {#each Array(8) as _, i}
              <li><button style="background-color: {colors[i + 8]};" class="btn btn-square btn-sm rounded-md" on:click={() => handleColorButtonClick(i + 8)}></button></li>
           {/each}
         </ul>
      </div>
      <div class="">
         <button class="btn btn-ghost w-20" on:click={handleChangeButtonClick}>
            {changeButtonText}
         </button>
      </div>
      {#if visible}
         <div class="absolute right-20 top-28 z-10">
            <input type="color" bind:value={inputHex} on:change={endChange} class="" />
        </div>
      {/if}
   </nav>
{/if}

<style>
   .nav-range {
      width: 180px;
      height: 20px;
      appearance: none;
      background-color: rgb(29, 29, 29);
      border-radius: 8px;
      outline: none;
      overflow: hidden;
   }
   .nav-range::-webkit-slider-thumb {
      -webkit-appearance: none;
      width: 5px;
      height: 20px;
      background-color: #A6ADBB;
      box-shadow: -340px 0px 0px 340px #A6ADBB;
   }
   .nav-range::-moz-range-thumb {
      -moz-appearance: none;
      width: 5px;
      height: 20px;
      background-color: #A6ADBB;
      box-shadow: -340px 0px 0px 340px #A6ADBB;
   }
</style>