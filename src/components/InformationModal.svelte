<script>
    import {fade} from "svelte/transition";

    export let title = "";
    export let shown;

    function closeModal(event) {
        event.preventDefault();
        if (event.target.id === "close")
            shown = false
    }
</script>

{#if shown}
    <div transition:fade="{{ duration: 200 }}" on:click={closeModal} id="close"
         style="background-color: rgba(20, 20, 20, 0.6);z-index:10;"
         class="fixed w-full h-full top-0 left-0 flex items-center justify-center overflow-scroll scrollbar-none">
        <div class="m-4 w-full sm:max-w-sm rounded-lg p-5 bg-white transition-all duration-200 shadow-lg">
            <div class="flex justify-between mb-2">
                <h1 class="text-gray-900 text-lg font-semibold">{@html title}</h1>
                <button on:click={closeModal} id="close">
                    <ion-icon id="close" name="close-circle-outline" class="my-auto pb-1 text-2xl focus:outline-none"></ion-icon>
                </button>
            </div>
            <slot/>
        </div>
    </div>
{/if}