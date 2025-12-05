
<script>
    import {users_store} from "$lib/user";
    let users = [];
	import {base} from '$app/paths';

    import { onMount } from 'svelte';
    onMount(() => {
        /*Check if has more then 2 characters*/
        if($users_store.length > 2){
            users = JSON.parse($users_store);
        }
        console.log(users)
    });

    function handleSubmit() {
        var keep_looking = true
        users.forEach(user => {
            if (keep_looking == true){
                if (user.username == name && user.email == email && user.password == password)
                    keep_looking = false
            }
        });

        if (keep_looking == false)
            alert("Välkommen, " + name + ", du är nu inloggad")
        else
            alert("Felaktig information eller obefintlig användare. Har du testat Logga In?")
    }
    let name = ""
    let email = ""
    let password = ""
    let color = "black"
    let colors = [{namn: "Blå", value: "blue"}, {namn: "Röd", value: "red"}, {namn: "Grön", value: "green"}, {namn: "Gul", value: "yellow"}]
    
</script>

<main>
    <div class="container">
        <h1>Inloggning</h1>
        <form on:submit|preventDefault={handleSubmit} class="formulär">
            <label for="name">Namn:</label>
            <input type="text" id="name" bind:value={name}>
            <label for="email">Email:</label>
            <input type="email" id="email" bind:value={email}>
            <label for="password">Lösenord:</label>
            <input type="password" id="password" bind:value={password}>
            <input type="submit" value="Logga in">
            <p>Har du inget konto? Testa <a href="{base}/register">registrera dig.</a></p>
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
