<script>
    import Tailwindcss from "./Tailwindcss.svelte";
    import Player from "./components/Player.svelte";
    import {writable} from "svelte/store";

    let name = "";

    let max = 13;
    let players = writable([]);

    let onlyOnce = [
        {id: 0, name: "Längste Handelsstraße", points: 2},
        {id: 1, name: "Größte Rittermacht", points: 2},
        {id: 2, name: "Hafenmeister", points: 2},
        {id: 3, name: "Größter Seeräuberschreck", points: 2},
        {id: -1, name: "BREAK", points: 0},
        {id: 4, name: "Handelsmetropole", points: 2},
        {id: 5, name: "Politikmetropole", points: 2},
        {id: 6, name: "Kulturmetropole", points: 2}
    ]

    function toggleCard(checked, id, playername) {
        if (checked === false)
          activateCard(id, playername)
        else
          deactivateCard(id, playername)
    }

    async function deactivateCard(id, playername) {
      const unsubscribe = players.subscribe(j => {
        j.forEach(p => {
          if (p.name !== playername)
            return;
          p.cards.forEach(card => {
            if (card.id !== id)
              return;

            card.active = false;
          });
        })
      })
      unsubscribe()
      // update view
      setTimeout(() => players = players, 100)
    }

    async function activateCard(id, playername) {
      const unsubscribe = players.subscribe(j => {
        j.forEach(p => {
          // remove active cards from other players
          if (p.name !== playername) {
            p.cards.forEach(card => {
              if (card.id !== id)
                return;

              card.active = false;
            });
          } else {
            // activate card for player
            p.cards.forEach(card => {
              if (card.id !== id)
                return;

              card.active = true;
            });
          }
        })
      })
      unsubscribe()
      // update view
      setTimeout(() => players = players, 100)
    }

    function addPlayer(event) {
        event.preventDefault();
        let cards = [];
        onlyOnce.forEach(card => {
            cards.push({...card, active: false})
            cards = cards;
        })
        $players = [...$players, {name: name, cards: cards}]
        name = "";
    }
</script>

<Tailwindcss/>
<main class="text-xl font-semibold m-2">
    {#if $players.length === 0}
        <p class="italic font-thin">Keine Spieler vorhanden</p>
    {/if}
    {#each $players as player}
        <Player {toggleCard} {player} cards={player.cards} {max}/>
    {/each}
    <div class="mt-12 flex justify-between text-base font-normal">
        <form on:submit={addPlayer}>
            <input bind:value={name} class="rounded my-1 px-1 border" placeholder="Name"/>
            <button class="text-sm text-white bg-blue-600 p-1 rounded" type="submit">Hinzufügen</button>
        </form>
        <div>
            <p>{max} max. SP</p>
            <div class="flex">
                <p class="my-auto mr-2">5</p>
                <input class="w-3/4" min="5" max="20" bind:value={max} type="range"/>
                <p class="my-auto ml-2">20</p>
            </div>
        </div>
    </div>
</main>
