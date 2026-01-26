<script>
    import { enhance } from "$app/forms";
    import ElizaBot from "elizabot";
    const eliza = new ElizaBot();
    let chat = $state([{user:'Eliza', message:eliza.getInitial()}]);

    
    async function write(sent_message) {
        //TODO: Add the new message to the chat
        chat.push({user:'You', message:sent_message})
        
        //Hämta HTML-elementet med id:et visible
        var element = document.getElementById("visible");
        //Ändrar elementets CSS-egenskap display till default
        element.style.display = "flex"; // Visa elementet

        // random delay for Eliza's response time
        await new Promise((r) => setTimeout(r, 1000 + Math.random() * 1000));

        //Ändrar elementets CSS-egenskap display till none
        element.style.display = "none" // Göm elementet

        //TODO: Add Eliza's response to the chat
        chat.push({user:'Eliza', message:eliza.transform(sent_message)})
  }
                

</script>

<main>
    <section>
        {#each chat as text}
            <article class:eliza_chat= {text.user=="Eliza"}>
                <p class:eliza_chat= {text.user=="Eliza"} data-time="12:34">{text.message}</p>
            </article>
        {/each}
        <article id = "visible">
            <span class = "circle"></span>
            <span class = "circle"></span>
            <span class = "circle"></span>
        </article>
    </section>
    <form method="post"
        use:enhance={({ formElement, formData, action, cancel }) => {
        cancel(); //don't post anything to server
        const text = formData.get("text"); // what does "text" refer to?
        write(text);

        formElement.reset()
        // TODO: reset the form using _____.reset() - what do we want to reset? the element or the data?

        }}>
        <input type="text" name="text" placeholder="Meddelande">
    </form>
                    
</main>

<style>
    article, input{
        margin: 10px;
        padding: 10px;
        border-radius: 10px;
        background-color: rgb(67, 115, 204);
        width: 90%;
        justify-items: end;
    }
    p::before {
        content: "You ";
        color: gold
    }
    p.eliza_chat::before {
        content: "Eliza ";
    }
    main{
        display: grid;
        width: 60vw;
        height: 70vh;
        justify-self: center;
        align-self: center;
        padding: 10px;
        border-radius: 10px;
        background-color: cornflowerblue;
        overflow-y: scroll;
    }
    #visible{
        width: 100px;
        height: 60px;
        display: none;
        justify-content: space-evenly;
        align-items: center;
        background-color: rgb(50, 80, 136);
    }
    @keyframes typing{
        0% {transform: scale(1);}
        50% {transform: scale(1.4);}
        100% {transform: scale(1);}
    }
    .circle{
        width: 10px;
        height: 10px;
        border-radius: 50%;
        background-color: aliceblue;
        
        animation-name: typing;
        animation-duration: 999ms;
        animation-timing-function: ease-in-out;
        animation-iteration-count: infinite;
    }
    .circle:nth-child(1) {
                animation-delay: 0ms; /* Ingen fördröjning */
            }
    /* CSS-stilar för .circle med index 2 (den andra cirkeln) */
    .circle:nth-child(2) {
        animation-delay: 333ms; /* Starta animationen efter 333 millisekunder (ms) */
    }
    /* CSS-stilar för .circle med index 3 (den tredje cirkeln) */
    .circle:nth-child(3) {
        animation-delay: 666ms; /* Starta animationen efter 666 ms */
    }
    article.eliza_chat {
        background-color: rgb(50, 80, 136);
        justify-items: start;
    }
    input {
        justify-items: start;
    }
</style>