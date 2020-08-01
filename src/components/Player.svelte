<script>
    import InformationModal from "./InformationModal.svelte";
    import Counter from "./Counter.svelte";
    import {writable} from "svelte/store";

    export let cards = [];
    export let toggleCard;
    export let player;
    export let max;

    $: {
      name = player.name;

      // calculate points
      points = 0;

      // for static cards
      cards.forEach((card, i) => {
        if (card.active)
          points += card.points
      });

      // for villages and towns
      points += villagePoints;
      points += townPoints;
      points += bonusPoints;
    }

    let name = "";
    let points = 0;
    let modal = false;

    let villages = writable(0);
    let towns = writable(0);
    let bonus = writable(0);

    let villagePoints = 0;
    let townPoints = 0;
    let bonusPoints = 0;
    villages.subscribe(value => villagePoints = value);
    towns.subscribe(value => townPoints = value*2);
    bonus.subscribe(value => bonusPoints = value);

    function openModal(event) {
        event.preventDefault();
        modal = false;
        modal = true;
    }
</script>

<InformationModal title="{name}" shown="{modal}">
    <div class="text-base font-normal">
        <div class="my-1">
          <Counter
            on:increment={() => {villages.update(n => n+1);}}
            on:decrement={() => {villages.update(n => n-1);}}
            value={$villages}
            max={5}/> {villagePoints === 1 ? "Dorf" : "Dörfer"} <span class="text-gray-500 italic">(1 Punkt)</span>
        </div>
        <div class="my-1">
          <Counter
            on:increment={() => {towns.update(n => n+1); villages.update(n => n-1);}}
            on:decrement={() => {towns.update(n => n-1);}}
            value={$towns}
            max={4}/> {townPoints === 2 ? "Stadt" : "Städte"} <span class="text-gray-500 italic">(2 Punkte)</span>
        </div>
        <hr class="my-2"/>
        {#each cards as card}
          {#if card.name === "BREAK"}
            <hr class="my-2"/>
          {:else}
            <label on:click={(event) => toggleCard(card.active, card.id, name)}>
                <input type="checkbox" class="my-1" active={card.active} bind:checked={card.active}/>
                {card.name} <span class="text-gray-500 italic">({card.points} Punkte)</span>
            </label><br/>
          {/if}
        {/each}
        <hr class="my-2"/>
        <div class="my-1">
          <Counter
            on:increment={() => {bonus.update(n => n+1);}}
            on:decrement={() => {bonus.update(n => n-1);}}
            value={$bonus}
            max={20}/> Extrapunkt{bonusPoints === 1 ? "" : "e"}
        </div>
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
        <div class="my-auto sm:w-1/5">
            <input type="range" min="0" max="{max}" bind:value={points} disabled/>
        </div>
    </div>
</a>
