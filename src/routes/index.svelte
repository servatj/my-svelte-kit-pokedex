<script>
    import { pokemon } from '../storage/pokestore';
    import PokemanCard from '../components/pokemanCard.svelte';
import About from './about.svelte';

    let searchTerm = "";
    let filteredPokemon = [];

    $: {
        if(searchTerm) {
            filteredPokemon = $pokemon.filter(pokeman => {
                return pokeman.name.toLowerCase().includes(searchTerm.toLocaleLowerCase());
            })
        } else {
            filteredPokemon = [...$pokemon ]
        }
    }
</script>
<svelte:head>
    <title>Svelte Kit Pokdex</title>
</svelte:head>
<h1 class="text-4xl text-center my-8 uppercase">Svelte kit polkadex</h1>

<input class="w-full rounder-md text-lg p-4 border-2 border-gray-200" bind:value={searchTerm} type="text" placeholder="Search Pokemon"/>
<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
    {#each filteredPokemon as pokeman}
        <PokemanCard pokeman={pokeman} />
    {/each}
</div>

<style>
    h1 {
        color: lightseagreen;
    }
</style>
