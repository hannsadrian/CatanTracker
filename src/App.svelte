<script>
    import Tailwindcss from "./Tailwindcss.svelte";
    import Player from "./components/Player.svelte";

    let name = "";

    let max = 13;
    let players = [];

    function addPlayer(event) {
        event.preventDefault();
        players.push({name: name})
        players = players;
        name = "";
    }
</script>

<Tailwindcss/>
<main class="text-xl font-semibold">
    {#if players.length === 0}
        <p class="italic font-thin">Keine Spieler vorhanden</p>
    {/if}
    {#each players as player}
        <Player {...player} {max}/>
    {/each}
    <div class="mt-12 flex justify-between text-base font-normal">
        <form on:submit={addPlayer}>
            <input bind:value={name} placeholder="Name"/>
            <button type="submit">Hinzufügen</button>
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
