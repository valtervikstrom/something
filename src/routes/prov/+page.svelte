<script>
    let box_amount = [1, 2, 3, 4, 5, 6]
</script>

<div class="main">
    <div class="squares">
        {#each box_amount as box}
            <div class="box"><p>{box}</p></div>
        {/each}
    </div>
</div>

<style>
    .box{
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: rgba(255, 255, 255, 0);
    }
    .squares{
        display: grid;

        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(2, 300%);
        grid-gap: 10px;
    }
    .squares .box:nth-child(6n-5){
        background-color: red;}
    .squares :nth-child(6n-4){
        background-color: blue;}
    .squares :nth-child(6n-3){
        background-color: green;}
    .squares :nth-child(6n-2){
        background-color: yellow;}
    .squares :nth-child(6n-1){
        background-color: purple;}
    .squares :nth-child(6n){
        background-color: #ffa500;}
    p{
        color: white;
    }
  
</style>