<script>
  import { createEventDispatcher } from 'svelte';

  export let value;
  export let max = 1000;
  const dispatch = createEventDispatcher();

  function increment() {
    if(value >= max)
      return;

    dispatch('increment', {value: value});
  }

  function decrement() {
    if (value < 1)
      return;

    dispatch('decrement', {value: value});
  }
</script>

<button on:click={decrement} class="rounded-lg text-sm bg-gray-400 hover:bg-gray-600 hover:text-white w-6 h-6">-</button>
{value}
<button on:click={increment} class="rounded-lg text-sm bg-gray-400 hover:bg-gray-600 hover:text-white w-6 h-6">+</button>
