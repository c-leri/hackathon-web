<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function click() {
		dispatch('click');
	}
</script>

<button class="btn variant-outline-surface w-full hover:variant-filled-surface" on:click={click}>
	<slot />
</button>
