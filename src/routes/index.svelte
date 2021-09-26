<script context="module">
	export async function load({ page }) {
		const url = 'https://pokeapi.co/api/v2/pokemon?limit=150';
		const res = await fetch(url);
		const data = await res.json();
		const loadedPokemon = data.results.map((pokemon, index) => {
			return {
				name: pokemon.name,
				id: index + 1,
				image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
					index + 1
				}.png`
			};
		});
        return { props: { pokemon: loadedPokemon }};
	}
</script>

<script>
	import PokemanCard from '../components/pokemanCard.svelte';
	export let pokemon;
    let searchTerm = '';
	let filteredPokemon = [];

	// use effect
	$: {
		if (searchTerm) {
			filteredPokemon = pokemon.filter((pokeman) => {
				return pokeman.name.toLowerCase().includes(searchTerm.toLocaleLowerCase());
			});
		} else {
			filteredPokemon = [...pokemon];
		}
	}
</script>

<svelte:head>
	<title>Svelte Kit Pokdex</title>
</svelte:head>
<h1 class="text-4xl text-center my-8 uppercase">Svelte kit polkadex</h1>

<input
	class="w-full rounder-md text-lg p-4 border-2 border-gray-200"
	bind:value={searchTerm}
	type="text"
	placeholder="Search Pokemon"
/>
<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
	{#each filteredPokemon as pokeman}
		<PokemanCard {pokeman} />
	{/each}
</div>

<style>
	h1 {
		color: lightseagreen;
	}
</style>
