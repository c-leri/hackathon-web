<script lang="ts">
	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import Item from '$lib/components/Item.svelte';

	let dynamicComponents: any[] = [Item, AddNewModule];
    export let moduleType: string;



	async function addItem() {
		dynamicComponents = [
			...dynamicComponents.slice(0, dynamicComponents.length - 1),
            Item,
			AddNewModule,
		
		];
	}
</script>

{#each dynamicComponents as element}
	{#if element === AddNewModule}
		<AddNewModule on:click={() => addItem()}>+</AddNewModule>
        {:else if element === Item}
		<Item bind:moduleType={moduleType} />
	 {:else}
		<svelte:component this={element} />
	{/if}
{/each}