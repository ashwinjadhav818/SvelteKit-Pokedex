<!-- ! Pokeman Cards -->
<script>
   import { fade } from 'svelte/transition';
   export let pokeman;
</script>

<a href={`/pokemon/${pokeman.name}`} class="list-none p-6 bg-gray-100 text-gray-800 text-center rounded-md shadow-sm hover:shadow-md flex flex-col items-center" transition:fade>
   <img src={pokeman.image} alt="{pokeman.name}" class="h-40 w-40 ">
   <h2 class="uppercase text-2xl">{pokeman.id}. {pokeman.name}</h2>
</a>