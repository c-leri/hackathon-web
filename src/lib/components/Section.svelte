<script lang="ts">
	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import MasterItem from '$lib/components/MasterItem.svelte';

	let dynamicComponents: any[] = [MasterItem];
	export let moduleType: string;

	async function addItem() {
		dynamicComponents = [...dynamicComponents, MasterItem];
	}
</script>

{#each dynamicComponents as element}
	{#if element === AddNewModule}
		<AddNewModule on:click={() => addItem()}>+</AddNewModule>
	{:else if element === MasterItem}
		<MasterItem {moduleType} />
	{:else}
		<svelte:component this={element} />
	{/if}
{/each}
