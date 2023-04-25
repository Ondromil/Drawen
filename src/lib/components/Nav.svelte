<script>
    export let index;

    function changeValue(value) {
        index = value;
    }
</script>

<nav class="navbar bg-slate-800">
   <div class="flex-none">
    <div class="dropdown">
       <button class="btn btn-square btn-ghost">
         <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-5 h-5 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path></svg>
       </button>
       <ul class="menu menu-compact dropdown-content mt-3 p-2 shadow bg-base-100 rounded-md w-40">
          <li><a>Save Project</a></li>
          <li><a>Clear</a></li>
          <li><a href="/about">About</a></li>
       </ul>
     </div>
    </div>
    <div class="flex-1">
       <p class="text-2xl ml-4">Drawen.io</p>
    </div>
    <div class="block mr-[100px]">
      <ul class="flex gap-1.5">
        <li><button class="bg-black btn btn-square btn-sm rounded-md hover:bg-black" on:click={() => changeValue(0)}></button></li>
        <li><button class="bg-white btn btn-square btn-sm rounded-md hover:bg-white" on:click={() => changeValue(1)}></button></li>
        <li><button class="bg-yellow-400 btn btn-square btn-sm rounded-md hover:bg-yellow-400" on:click={() => changeValue(2)}></button></li>
        <li><button class="bg-blue-600 btn btn-square btn-sm rounded-md hover:bg-blue-600" on:click={() => changeValue(3)}></button></li>
        <li><button class="bg-red-600 btn btn-square btn-sm rounded-md hover:bg-red-600" on:click={() => changeValue(4)}></button></li>
        <li><button class="bg-green-500 btn btn-square btn-sm rounded-md hover:bg-green-500" on:click={() => changeValue(5)}></button></li>
        <li><button class="bg-slate-400 btn btn-square btn-sm rounded-md hover:bg-slate-400" on:click={() => changeValue(6)}></button></li>
        <li><button class="bg-orange-400 btn btn-square btn-sm rounded-md hover:bg-orange-400" on:click={() => changeValue(7)}></button></li>
      </ul>
      <ul class="flex gap-1.5">
        <li><button class="bg-purple-600 btn btn-square btn-sm rounded-md hover:bg-purple-600" on:click={() => changeValue(8)}></button></li>
        <li><button class="bg-amber-700 btn btn-square btn-sm rounded-md hover:bg-amber-700" on:click={() => changeValue(9)}></button></li>
        <li><button class="bg-lime-400 btn btn-square btn-sm rounded-md hover:bg-lime-400" on:click={() => changeValue(10)}></button></li>
        <li><button class="bg-blue-400 btn btn-square btn-sm rounded-md hover:bg-blue-400" on:click={() => changeValue(11)}></button></li>
        <li><button class="bg-pink-400 btn btn-square btn-sm rounded-md hover:bg-pink-400" on:click={() => changeValue(12)}></button></li>
        <li><button class="bg-green-800 btn btn-square btn-sm rounded-md hover:bg-green-800" on:click={() => changeValue(13)}></button></li>
        <li><button class="bg-teal-400 btn btn-square btn-sm rounded-md hover:bg-teal-400" on:click={() => changeValue(14)}></button></li>
        <li><button class="bg-indigo-600 btn btn-square btn-sm rounded-md hover:bg-indigo-600" on:click={() => changeValue(15)}></button></li>
      </ul>
    </div>
    <div class="flex-none">
       <button class="btn btn-square btn-ghost">
         <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-5 h-5 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z"></path></svg>
       </button>
   </div>
  </nav>