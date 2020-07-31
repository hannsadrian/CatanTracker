<script>
    import Tailwindcss from "./Tailwindcss.svelte";
    import Player from "./components/Player.svelte";
    import {writable} from "svelte/store";

    let name = "";

    let max = 13;
    let players = [];

    let onlyOnce = [
        {id: 0, name: "Längste Handelsstraße", points: 2},
        {id: 1, name: "Größte Rittermacht", points: 2},
        {id: 2, name: "Hafenmeister", points: 2},
        {id: 3, name: "Größter Räuberschreck", points: 2}
    ]

    function activateCard(id, player, cards) {
        console.log(id)
        console.log(player)
        players.forEach(p => {
            p.subscribe(s => {
                console.log(s)
            })
        })
    }

    function addPlayer(event) {
        event.preventDefault();
        let cards = [];
        onlyOnce.forEach(card => {
            cards.push({...card, active: false})
            cards = cards;
        })
        players.push(writable({name: name, cards: cards}))
        players = players;
        name = "";
    }
</script>

<Tailwindcss/>
<main class="text-xl font-semibold m-2">
    {#if players.length === 0}
        <p class="italic font-thin">Keine Spieler vorhanden</p>
    {/if}
    {#each players as player}
        <Player {activateCard} {player} {max}/>
    {/each}
    <div class="mt-12 flex justify-between text-base font-normal">
        <form on:submit={addPlayer}>
            <input bind:value={name} class="rounded px-1 border" placeholder="Name"/>
            <button class="text-sm text-white bg-blue-600 p-1 rounded" type="submit">Hinzufügen</button>
        </form>
        <div>
            <p>{max} maximale Siegpunkte</p>
            <div class="flex">
                <p class="my-auto mr-2">5</p>
                <input class="w-3/4" min="5" max="20" bind:value={max} type="range"/>
                <p class="my-auto ml-2">20</p>
            </div>
        </div>
    </div>
</main>
