<script context="module">
   export async function load({page}) {
      const id = page.params.id;
      const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
      const res = await fetch(url);
      const pokeman = await res.json();

      return {
         props: {pokeman}
      };
   };
</script>

<script>
   export let pokeman;
   const type = pokeman.types[0].type.name;
   const name = pokeman.name.toUpperCase();
</script>

<svelte:head>
   <title>Pokedex | {name}</title>
</svelte:head>

<div class="flex flex-col items-center">
   <h1 class="text-4xl text-center my-8 uppercase">{pokeman.name}</h1>
   <img class="card-image h-40 w-40" src={pokeman.sprites['front_default']} alt={pokeman.name}/>
   <p class="uppercase">Type: <strong>{type}</strong> | Height: <strong>{pokeman.height}</strong>
      | Weight: <strong>{pokeman.weight}</strong>
   </p>
</div>