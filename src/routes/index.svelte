<!-- ! Home Page -->
<script>
   import { pokemon } from '../stores/pokestore';
   import PokemanCard from '../Components/pokemanCard.svelte';
   
   let searchTerm = "";
   let filteredPokemon = [];

   $: {
      if (searchTerm) {
         filteredPokemon = $pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLocaleLowerCase()));
      } else {
         filteredPokemon = [...$pokemon]
      }
   }
</script>

<svelte:head>
	<title>Pokedex | Home</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">Pokedex</h1>

<input type="text" placeholder="Search Pokemon" class="w-full rounded-md text-lg p-4 border-2 border-gray-200" bind:value={searchTerm}>

<div class="grid gap-4 md:grid-cols-2 grid-cols-1 mt-4">
   {#each filteredPokemon as pokeman}
      <PokemanCard pokeman={pokeman} />
   {/each}
</div>
