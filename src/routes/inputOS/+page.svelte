<script>
	let top = $state(Math.floor(Math.random()*500));
	let left = $state(Math.floor(Math.random()*500));
    let targets = $state([0, 0, 0])
    let timer_start = Date.now()
    let timer_now = Date.now()
    let timer_final = $state(timer_now-timer_start)
    let timer_penalty = $state(0)
	// up = 38
	// down = 40
	// right = 39
	// left = 37
	function onKeyDown(e) {
		switch(e.keyCode) {
			case 39:
				left += Math.floor(Math.random()*7)+2;
				break;
            case 37:
                left -= Math.floor(Math.random()*7)+2;
                break;
            case 40:
				top += Math.floor(Math.random()*7)+2;
				break;
            case 38:
                top -= Math.floor(Math.random()*7)+2;
                break;
            case 32:
                if (check_hit() != 3){
                    console.log(check_hit())
                    targets[check_hit()] = 1
                }
                if (check_hit() != 0 && check_hit() != 1 && check_hit() != 2)
                    timer_penalty += 5000
                break
		}
        timer_now = Date.now()
        timer_final = (timer_now - timer_start + timer_penalty)/1000
	}

    function check_hit(){
        let targets = document.getElementsByClassName("target")
        let aim = document.getElementsByClassName("aim")[0].getBoundingClientRect()
        let target_finder = 0
        for (let t of targets){
            let temp_t = t.getBoundingClientRect()
            if (Math.abs((temp_t.x+temp_t.width/2)-(aim.x+aim.width/2))<8.5 && Math.abs((temp_t.y+temp_t.width/2)-(aim.y+aim.width/2))<8.5)
                var target_found = target_finder
            target_finder+=1
        }
        return target_found
    }
</script>
<style>
    h1 {
        justify-self: center;
    }
	main {
		width: 500px;
		height: 500px;
		border: solid blue 1px;
		margin: 10px auto;
		position: relative
	}
	.aim {
		width: 6px;
		height: 5px;
        border-radius: 50%;
		background-color: red;
		position: absolute;
	}
    .aim_outer {
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border-style: solid;
        border-width: 2px;
        border-color: red;
        position: absolute;
    }
    .targets {
        width: 500px;
        height: 483px;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
    .target {
        width: 10px;
		height: 10px;
        border-radius: 50%;
    }
</style>

<h1>{timer_final}</h1>
<main>
    <div class='targets'>
        {#each targets as i}
            {#if i==0}
                <aside class='target' style="background-color: black;"></aside>
            {/if}
            {#if i==1}
                <aside class='target' style="background-color: green;"></aside>
            {/if}
        {/each}
    </div>
	<div class='aim' style="left: {left-1}px; top: {top-1}px"></div>
    <div class='aim_outer' style="left: {left-10}px; top: {top-10}px"></div>
</main>

<svelte:window on:keydown|preventDefault={onKeyDown} />