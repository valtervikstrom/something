<script>
    let numbers_box = $state([[1, 2, 3], [4, 5, 6], [7, 8, 9, 0]])
    let phone_number = $state([])
    function gamble1(){
        numbers_box[0].forEach(element => {
            numbers_box[0].push(Math.floor(Math.random()*10))
            numbers_box[0].shift()
        });
    }
    function gamble2(){
        numbers_box[1].forEach(element => {
            numbers_box[1].push(Math.floor(Math.random()*10))
            numbers_box[1].shift()
        });
    }
    function gamble3(){
        numbers_box[2].forEach(element => {
            numbers_box[2].push(Math.floor(Math.random()*10))
            numbers_box[2].shift()
        });
    }
    function gamble_submit(){
        let phone_num_ph = []
        numbers_box.forEach(element => {
            element.forEach(element => {
                phone_num_ph.push(element)
            })
        });
        phone_number = phone_num_ph
    }

    let symbols = []
</script>

<main>
    <h1>Register new account</h1>
    <p>Please enter your phone number below</p>
    <div class='Number'>
        <div class='Number'>{#each numbers_box[0] as i}
            <div>{i}</div>
        {/each}</div>
        <input type='button' onclick={gamble1}>
        <div class='Number'>{#each numbers_box[1] as i}
            <div>{i}</div>
        {/each}</div>
        <input type='button' onclick={gamble2}>
        <div class='Number'>{#each numbers_box[2] as i}
            <div>{i}</div>
        {/each}</div>
        <input type='button' onclick={gamble3}>
    </div>
    <form onsubmit={gamble_submit}>
        <input type="submit" value="Submit">
    </form>

    <p>Please enter your email adress below</p>
    <div class='email'>

    </div>
</main>

<style>
    main{
        justify-self: center;
    }
    .Number{
        display: flex;
        flex-direction: row;
    }
    .email{
        border-color: black;
        border: solid;
        border-width: 2px;
        height: 300px;
        width: 600px;
        background-color: rgb(200, 200, 200);
    }
</style>