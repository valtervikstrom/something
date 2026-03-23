
<script>
  /** @type {import('./$types').PageData} */
  export let data;

</script>

{#await data}
  <p>.. waiting</p>
{:then pokemon} 

<article class="pictures">
    {#each Object.entries(pokemon.response.sprites) as sprites}
    {#if typeof sprites[1] == "string"}
        <img src={sprites[1]} alt={pokemon.response.name}/>
    {/if}
    {/each}
</article>


<article class="abilities">
    <p>Abilities: </p>
    {#each pokemon.response.abilities as ability_holder}
        <p>{ability_holder.ability.name}</p>
    {/each}
</article>

<article class="types">
    <p>Types: </p>
        {#each pokemon.response.types as types}
            <p>{types.type.name}</p>
        {/each}
</article>

<article class="stats">
    <p>Stats: </p>
    {#each pokemon.response.stats as stat}
        <p>{stat.stat.name}: {stat.base_stat}</p>
    {/each}
</article>

<h1>{pokemon.response.name}</h1>
<section>

</section>

{/await}  


<style>
    .pictures {
        display: flex;
        justify-content: center;
        width: 90%;
        height: 30%;
        gap: 1em;
        max-width: 100%;
    }
    .abilities {
        display: flex;
        flex-direction: row;
        gap: 20px
    }
    .types {
        display: flex;
        flex-direction: row;
        gap: 10px;
    }
    .stats {
        display: flex;
        flex-direction: row;
        gap: 10px;
    }
</style>