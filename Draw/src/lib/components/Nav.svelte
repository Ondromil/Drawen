<script>
    import { createEventDispatcher } from "svelte";

    function func(par) {
        console.log("penis" + par)
    }
</script>

<nav class="navbar bg-slate-800">
   <div class="flex-none">
     <button class="btn btn-square btn-ghost">
       <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-5 h-5 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path></svg>
     </button>
    </div>
    <div class="flex-1">
       <a class="text-2xl ml-4">Drawen.io</a>
    </div>
    <div class="block mr-[100px]">
      <ul class="flex gap-1.5">
        <li><button class="bg-black btn btn-square btn-sm rounded-md hover:bg-black" ></button></li>
        <li><button class="bg-white btn btn-square btn-sm rounded-md hover:bg-white"></button></li>
        <li><button class="bg-yellow-400 btn btn-square btn-sm rounded-md hover:bg-yellow-400" on:click={() => func("lol")}></button></li>
        <li><button class="bg-blue-600 btn btn-square btn-sm rounded-md hover:bg-blue-600"></button></li>
        <li><button class="bg-red-600 btn btn-square btn-sm rounded-md hover:bg-red-600"></button></li>
        <li><button class="bg-green-500 btn btn-square btn-sm rounded-md hover:bg-green-500"></button></li>
        <li><button class="bg-slate-400 btn btn-square btn-sm rounded-md hover:bg-slate-400"></button></li>
        <li><button class="bg-orange-400 btn btn-square btn-sm rounded-md hover:bg-orange-400" ></button></li>
      </ul>
      <ul class="flex gap-1.5">
        <li><button class="bg-purple-600 btn btn-square btn-sm rounded-md hover:bg-purple-600"></button></li>
        <li><button class="bg-amber-700 btn btn-square btn-sm rounded-md hover:bg-amber-700"></button></li>
        <li><button class="bg-lime-400 btn btn-square btn-sm rounded-md hover:bg-lime-400"></button></li>
        <li><button class="bg-blue-400 btn btn-square btn-sm rounded-md hover:bg-blue-400"></button></li>
        <li><button class="bg-pink-400 btn btn-square btn-sm rounded-md hover:bg-pink-400"></button></li>
        <li><button class="bg-green-800 btn btn-square btn-sm rounded-md hover:bg-green-800"></button></li>
        <li><button class="bg-teal-400 btn btn-square btn-sm rounded-md hover:bg-teal-400"></button></li>
        <li><button class="bg-indigo-600 btn btn-square btn-sm rounded-md hover:bg-indigo-600" ></button></li>
      </ul>
    </div>
    <div class="flex-none">
       <button class="btn btn-square btn-ghost">
         <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-5 h-5 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z"></path></svg>
       </button>
   </div>
  </nav>