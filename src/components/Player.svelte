<script>
    import InformationModal from "./InformationModal.svelte";

    export let cards = [];
    export let toggleCard;
    export let player;
    export let max;

    $: {
      name = player.name;

      // calculate points
      points = 0;

      cards.forEach((card, i) => {
        if (card.active)
          points += card.points
      });

    }

    let name = "";
    let points = 0;
    let modal = false;

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
</script>

<InformationModal title="{name}" shown="{modal}">
    <div class="text-base font-normal">
        {#each cards as card}
            <label on:click={(event) => toggleCard(card.active, card.id, name)}>
                <input type="checkbox" class="my-1" active={card.active} bind:checked={card.active}/>
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
