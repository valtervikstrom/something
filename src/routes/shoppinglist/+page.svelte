<script>
    import { preventDefault } from "svelte/legacy";
    import { fade } from 'svelte/transition'
    function listSubmit(e) {
        e.preventDefault()
        if (ny_vara != "")
            if (priority != "")
                varor.push({name:ny_vara, state:"buy", prioritet:priority});
            if (priority == "")
                varor.push({name:ny_vara, state:"buy", prioritet:0});
    }
    function listSwapBought(e) {
        e.preventDefault()
        var shouldStopA = false
        varor.forEach(vara => {
            if (vara.name == köpt_vara && vara.state == "buy" && shouldStopA == false){
                vara.state = "bought"
                shouldStopA = true
            }
        });
    }
    function listSwapBuy(e) {
        e.preventDefault()
        var shouldStopB = false
        varor.forEach(vara => {
            if (vara.name == köpt_vara && vara.state == "bought" && shouldStopB == false){
                vara.state = "buy"
                shouldStopB = true
            }
        });
    }
    let varor = $state([{}]);
    $effect(() => {
        varor.forEach(vara1 => {
            varor.forEach(vara2 => {
                varor.sort((vara1, vara2) => vara1.prioritet - vara2.prioritet)
            })
        })
    })
    let ny_vara = $state("")
    let priority = $state("")
    let köp_vara = $state("")
    let köpt_vara = $state("")
</script>

<main class="container">
    <h1>Shoppinglist</h1>
    <div class="categories_container">
        <section>
            <h2>Varor att köpa</h2>
            <ol>
                {#each varor as vara}
                    {#if vara.state == "buy"}
                        <li transition:fade>{vara.name}</li>
                    {/if}
                {/each}
            </ol>
        </section>
        <section>
            <h2>Köpta varor</h2>
            <ul>
                {#each varor as vara}
                    {#if vara.state == "bought"}
                        <li transition:fade>{vara.name}</li>
                    {/if}
                {/each}
            </ul>
        </section>
    </div>    
    <div class="commands">
        <form onsubmit={listSwapBought} class="listform">
            <label for="köpt_vara">Köpt vara:</label>
            <input type="text" id="köpt_vara" bind:value={köpt_vara}>
            <input type="submit" value="Flytta">
        </form>
        <form onsubmit={listSubmit} class="listform">
            <label for="ny_vara">Ny vara:</label>
            <input type="text" id="ny_vara" bind:value={ny_vara}>
            <label for="priority">Prioritet:</label>
            <input type="number" id="priority" bind:value={priority}>
            <input type="submit" value="Lägg till">
        </form>
        <form onsubmit={listSwapBuy} class="listform">
            <label for="köp_vara">Ej köpt vara:</label>
            <input type="text" id="köp_vara" bind:value={köp_vara}>
            <input type="submit" value="Flytta">
        </form>
    </div>
</main>

<style>
    .container{
        background-color: blueviolet;
        width: 100vw;
        height: 98vh;
        border-radius: 20px;
        display: grid;
        grid-template-rows: 1fr 9fr 1fr;
    }
    .categories_container{
        height: 100%;
        background-color: rgb(150, 0, 90);
        display: grid;
        grid-template-columns: repeat(2, 1fr);
    }

    h1{
        border-radius: 20px;
        background-color: darkmagenta;
    }

    .container h1{
        align-self: center;
        justify-self: center;
    }

    h2{
        background-color: rgba(0, 0, 0, 0.1);
        font-size: 25px;
        text-align: center;
        padding: 10px;
        margin-top: 0%;
    }

    section{
        size: 100%;
    }
    
    .categories_container section:nth-child(odd){  /* vilket barn vill vi styla? */
        background-color: rgba(0, 0, 0, 0.1); /* svart bakgrund med 10% opacitet */
    }
 
    .categories_container section:nth-child(even){  /* vilket barn vill vi styla? */
        background-color: rgba(0, 0, 0, 0.3); /* svart bakgrund med 30% opacitet */
    }

    .commands{
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        align-self: center;
    }
    
    li{
        border-style: none none solid none;
        border-bottom-width: 1px;
        border-bottom-color: black;
    }


 
    
</style>