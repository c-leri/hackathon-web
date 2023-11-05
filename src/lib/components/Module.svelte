<script lang="ts">
	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import TitleModule from '$lib/components/TitleModule.svelte';
    import Section from '$lib/components/Section.svelte';

    export let moduleType: string;

	let dynamicComponents: any[] = [TitleModule, AddNewModule];

	async function addDynamicComponent(index: number) {
		dynamicComponents = [
			...dynamicComponents.slice(0, index + 1),
			Section,
			...dynamicComponents.slice(index + 1)
		];
	}
</script>

<h1>{moduleType}</h1>

{#each dynamicComponents as element, index (index)}
	{#if element === AddNewModule}
		{index}
		<AddNewModule on:click={() => addDynamicComponent(index)}>Ajouter une section</AddNewModule>
    {:else if element === Section}
		<Section bind:moduleType={moduleType} />
        {:else}
		<svelte:component this={element} />
	{/if}
{/each}
