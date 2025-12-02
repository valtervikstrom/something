<h1>Photoapp</h1>
<p>Denna sida innehåller <b>fina</b> bilder</p>

<script>
    let image = "https://picsum.photos/id/70/367/267"
    let photo = "https://picsum.photos/id/88/367/267"
    let picture = "https://picsum.photos/id/93/367/267"
</script>

<div class="photos">
    <div class="image-wrapper">
    <img src={image} alt="Flexbox egenskaper">
    </div>
    <div class="image-wrapper">
    <img src={photo} alt="Flexbox">
    </div>
    <div class="image-wrapper">
    <img src={picture} alt="Flexbox">
    </div>
</div>
<style>
    .image-wrapper img{ 
        width: 100%; 
        height: 100%;
        border-radius: 20px;
        box-shadow: 4px 8px 10px rgba(0, 0, 0, 0.2);
    }
    .image-wrapper{
        flex-grow: 1;
        margin: 10px;
        height: 50vh;
        flex-basis: 300px;
    }
    .image-wrapper:hover {flex-grow: 2;}
    .image-wrapper:active { transform: scale(0.9); }
    .photos{
        display:flex;
        max-width: 90vw;
        overflow:hidden;
        width: 100%;
        align-items: center;
        justify-content: center;
        flex-wrap: wrap;
    }
    h1{
        text-align: center;
        font-size: 50px;
        margin: 20px;
        color: grey;
    }
    
</style>