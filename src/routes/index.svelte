<!-- ! Home Page -->
<script context="module">
   export async function load({page}) {
      const url = `https://pokeapi.co/api/v2/pokemon/?limit=500`;
      const res = await fetch(url);
      const data = await res.json();
      const loadedPokemon = data.results.map((data, index) => {
         return {
            name: data.name,
            id: index + 1,
            image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1
               }.png`
         };
      });
      return {
         props: {pokemon:loadedPokemon}
      };
   };
</script>

<script>
   import PokemanCard from '../Components/pokemanCard.svelte';
   import { fade } from 'svelte/transition';
   export let pokemon;
   
   let searchTerm = "";
   let filteredPokemon = [];

   $: {
      if (searchTerm) {
         filteredPokemon = pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLocaleLowerCase()));
      } else {
         filteredPokemon = [...pokemon]
      }
   }
</script>

<svelte:head>
	<title>Pokedex | Home</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase" transition:fade>Pokedex</h1>

<input type="text" placeholder="Search Pokemon" class="w-full rounded-md text-lg p-4 border-2 border-gray-200" bind:value={searchTerm} transition:fade>

<div class="grid gap-4 md:grid-cols-2 grid-cols-1 mt-4">
   {#each filteredPokemon as pokeman}
      <PokemanCard pokeman={pokeman} />
   {/each}
</div>
