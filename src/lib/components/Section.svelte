<script lang="ts">
	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import MasterItem from '$lib/components/MasterItem.svelte';

	let dynamicComponents: any[] = [MasterItem, AddNewModule];
    export let moduleType: string;



	async function addItem() {
		dynamicComponents = [
			...dynamicComponents.slice(0, dynamicComponents.length - 1),
            MasterItem,
			AddNewModule,
		
		];
	}
</script>

{#each dynamicComponents as element}
	{#if element === AddNewModule}
		<AddNewModule on:click={() => addItem()}>+</AddNewModule>
        {:else if element === MasterItem}
		<MasterItem moduleType={moduleType} />
	 {:else}
		<svelte:component this={element} />
	{/if}
{/each}