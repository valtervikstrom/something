
<script>    
    import {users_store} from "$lib/user";
    let users = [];
    
    import { onMount } from 'svelte';
    onMount(() => {
        /*Check if has more then 2 characters*/
        if($users_store.length > 2){
            users = JSON.parse($users_store);
        }
    });

	import { preventDefault } from "svelte/legacy";
    function handleSubmit() {
        let current_user = users.find(user => user.name == name)
        if (current_user.name == name)
            alert("Användarnamn används redan");
        else
            alert("Välkommen " + name + " " + email + " " + password + " " + color)
                
            let new_user = {username: name, password: password, email: email, color: color};
            users = [...users, new_user];
            $users_store = JSON.stringify(users);
    }
    let name = ""
    let email = ""
    let password = ""
    let color = "black"
    let colors = [{namn: "Blå", value: "blue"}, {namn: "Röd", value: "red"}, {namn: "Grön", value: "green"}, {namn: "Gul", value: "yellow"}]
    
</script>

<main>
    <div class="container">
        <h1>Registrering</h1>
        <form on:submit|preventDefault={handleSubmit} class="formulär">
            <div style="width: 100px; height: 100px; border-radius: 50%; overflow:hidden; background-color:{color};"></div>
            <label for="name">Namn:</label>
            <input type="text" id="name" bind:value={name}>
            <label for="email">Email:</label>
            <input type="email" id="email" bind:value={email}>
            <label for="password">Lösenord:</label>
            <input type="password" id="password" bind:value={password}>
            <label for="color"> Favoritfärg:</label>
            <select id ="color" bind:value={color}>
                {#each colors as c}
                    <option value={c.value}>{c.namn}</option>
                {/each}
            </select>
            <input type="submit" value="Registrera">
            <p>Har du redan ett konto? Testa <a href="{base}/login">logga in.</a></p>
        </form>
    </div>
</main>

<style>
    main{
        background-image: url("https://t4.ftcdn.net/jpg/05/21/65/59/360_F_521655929_N80d5GaCQJ2VP073PfTXJTe9mkvsNtHE.jpg");
        background-size: cover;
        width: 100%;
        height: 100%;
        padding: 5%;
        min-height: 500px;
    }
    .container{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-evenly;
        border: solid 5px rosybrown;
        border-radius: 10px;
        width: 25%;
        height: 70%;
        background-color: #3a2e3b;
        margin: auto;
        min-width: 300px;
        min-height: 500px;
    }
    .formulär{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-items: center;
    }
</style>
