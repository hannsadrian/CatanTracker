<script>
    import InformationModal from "./InformationModal.svelte";

    export let activateCard;
    export let player;
    export let max;

    let name = "";
    let points = 0;
    let modal = false;

    let cards = [];

    function openModal(event) {
        event.preventDefault();
        modal = false;
        modal = true;
    }

    function increaseScore() {
        if (points < max)
            points++;
    }

    function decreaseScore() {
        if (points > 0)
            points--;
    }

    player.subscribe(p => {
        name = p.name;
        cards = p.cards;
    })
</script>

<InformationModal title="{name}" shown="{modal}">
    <div class="text-base font-normal">
        {#each cards as card}
            <label on:click={activateCard.bind({}, card.id, name, cards)}>
                <input type="checkbox" class="my-1" checked={card.active}/>
                {card.name}
            </label><br/>
        {/each}
    </div>
</InformationModal>
<a href on:click={openModal}>
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
</a>
