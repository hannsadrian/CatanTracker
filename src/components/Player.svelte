<script>
    export let name;
    export let max;

    let points = 0;

    function increaseScore() {
        if (points < max)
            points++;
    }

    function decreaseScore() {
        if (points > 0)
            points--;
    }

    $: {
        if (points > max)
            points = max;
    }
</script>

<div class="flex justify-between my-2">
    <div>
        <h2 class="-mb-2 leading-tight">{name}</h2>
        {#if points >= max}
            <p class="font-normal">Gewonnen!</p>
            {:else}
        <p class="font-thin italic">{points} Punkte</p>
            {/if}
    </div>
    <div class="my-auto flex">
        <button class="w-8 my-auto mx-2" on:click="{decreaseScore}">-</button>
        <input type="range" min="0" max="{max}" bind:value={points}/>
        <button class="w-8 my-auto mx-2" on:click="{increaseScore}">+</button>
    </div>
</div>