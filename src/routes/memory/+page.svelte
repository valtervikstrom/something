<script>
    let cards = $state([{image: "https://picsum.photos/id/93/367/267", flipped: false, matched: false}, {image: "https://greggvanourek.com/wp-content/uploads/2023/08/Nature-path-by-water-trees-and-mountains-AdobeStock_291242770-768x463.jpeg", flipped: false, matched: false}, {image: "https://onetreeplanted.org/cdn/shop/articles/nature_facts_1788x.jpg?v=1761073103", flipped: false, matched: false}, {image: "https://blog.3bee.com/_next/image/?url=https%3A%2F%2Fapi-backend-assets.s3.eu-south-1.amazonaws.com%2Fprivate%2Ffiler_public%2Fb8%2F5c%2Fb85c004f-8f5d-4b6c-ab70-25051c3fb9ba%2F11496fd2-2abf-4037-8b09-9627a1e60a3c.jpg&w=3840&q=75", flipped: false, matched: false}, {image: "https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/file-uploads/blogs/15271/images/2c2e3-b62b-f276-faa8-57cc871762_Kingley-Vale-West-Sussex-England.jpg", flipped: false, matched: false}, {image: "https://wallpapers.com/images/featured/cool-nature-bilder-pqezbkindvbvu0ow.jpg", flipped: false, matched: false}, {image: "https://picsum.photos/id/93/367/267", flipped: false, matched: false}, {image: "https://greggvanourek.com/wp-content/uploads/2023/08/Nature-path-by-water-trees-and-mountains-AdobeStock_291242770-768x463.jpeg", flipped: false, matched: false}, {image: "https://onetreeplanted.org/cdn/shop/articles/nature_facts_1788x.jpg?v=1761073103", flipped: false, matched: false}, {image: "https://blog.3bee.com/_next/image/?url=https%3A%2F%2Fapi-backend-assets.s3.eu-south-1.amazonaws.com%2Fprivate%2Ffiler_public%2Fb8%2F5c%2Fb85c004f-8f5d-4b6c-ab70-25051c3fb9ba%2F11496fd2-2abf-4037-8b09-9627a1e60a3c.jpg&w=3840&q=75", flipped: false, matched: false}, {image: "https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/file-uploads/blogs/15271/images/2c2e3-b62b-f276-faa8-57cc871762_Kingley-Vale-West-Sussex-England.jpg", flipped: false, matched: false}, {image: "https://wallpapers.com/images/featured/cool-nature-bilder-pqezbkindvbvu0ow.jpg", flipped: false, matched: false}])
    let bluePoints = $state(0)
    let blueTurn = $state(true)
    let redPoints = $state(0)
    var flipCount = 0
    var flipTrack = []

    function flip(i) {
        if (flipCount >=2 || i.flipped)
            return
        i.flipped = true
        flipCount += 1
        flipTrack.push(i)
        if (flipCount >= 2){
            if (flipTrack[0].image == flipTrack[1].image){
                cards.forEach(element => {
                    if (element.flipped == true)
                        element.matched = true;
                })
                if (blueTurn)
                    bluePoints += 1;
                else
                    redPoints += 1;
                flipTrack = [];
                flipCount = 0;
            }
        }}
    
    function pass() {
        cards.forEach(element => {
            if (element.matched == false)
                element.flipped = false;
        });
        if (flipTrack[0].image != flipTrack[1].image){
            if (blueTurn)
                blueTurn = false
            else
                blueTurn = true
        }
        flipTrack = [];
        flipCount = 0;
    }

    function reset() {
        cards.forEach(element => {
            element.matched = false
            element.flipped = false
        })
        bluePoints = 0
        redPoints = 0
        flipTrack = [];
        flipCount = 0;
    }
</script>

<h1>Memory</h1>
<main>
    {#each cards as i}
        <div class="card" class:flipped= {i.flipped} onclick={()=>flip(i)}>
            <img src={i.image} alt="front" class="front">
            <img src="https://picsum.photos/id/88/367/267" alt="back" class="back">
        </div>
    {/each}
</main>

<form onsubmit={pass}>
    <input type="submit" value="Pass">
</form>
<form onsubmit={reset}>
    <input type="submit" value="Restart">
</form>

<aside>
    <p>{redPoints}</p>
</aside>

<aside class="blue">
    <p>{bluePoints}</p>
</aside>

<aside class="turn" class:blue= {blueTurn}></aside>

<style>
    form{
        justify-self: center;
        margin-top: 10px;
    }
    h1{
        justify-self: center;
    }
    main{
        display: grid;
        grid-template-columns:repeat(4, 100px);
        grid-template-rows:repeat(3, 100px);
        justify-content: center;
    }
    .card{
        border-style: solid;
        border-width: 1px;
        height: 100%;
        width: 100%;
        position: relative;
        
        transform-style: preserve-3d;
        transition: transform 0.5s ease;
    }
    aside{
        width: 100px;
        height: 100px;
        position: fixed;
        bottom: 10px;
        right: 10px;
        background-color: red;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .blue{
        background-color: blue;
        left: 10px;
    }
    p{
        font-size: 30px;
    }
    .turn{
        box-shadow: 0 0 10px purple;
        z-index: -1;
    }
    .front,.back{
      width: 100%;
        height: 100%;
        position: absolute;  
        left: 0;
        top:0; 
        backface-visibility: hidden;
    }
    .front{
       
        transform: rotateY(180deg);
    }
    .back{
       
        transform: rotateY(0deg);
    }
    .flipped{
        transform: rotateY(180deg);
    }
</style>