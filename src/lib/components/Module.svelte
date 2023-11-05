<script lang="ts">
	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import TitleModule from '$lib/components/TitleModule.svelte';
	import Section from '$lib/components/Section.svelte';
	import Icon from '@iconify/svelte';

	export let moduleType: string;

	//Ugly way to disconnect module and its children from page
	const endModule = moduleType;

	let dynamicComponents: { id: number; element: any }[] = [];

	async function addDynamicComponent() {
		dynamicComponents = [...dynamicComponents, { id: dynamicComponents.length, element: Section }];
	}

	function removeDynamicComponent(id: number) {
		dynamicComponents = [
			...dynamicComponents.filter((dynamicComponent) => dynamicComponent.id !== id)
		];
	}
</script>

<h1>{endModule}</h1>

<TitleModule />
<AddNewModule on:click={() => addDynamicComponent()}>Ajouter une section</AddNewModule>
{#each dynamicComponents as dynamicComponent (dynamicComponent.id)}
	{#if dynamicComponent.element === Section}
		<Section moduleType={endModule} />
	{:else}
		<svelte:component this={dynamicComponent.element} />
	{/if}
	<div class="print:hidden">
		<button
			class="btn-icon variant-outline-error hover:variant-filled-error"
			on:click={() => removeDynamicComponent(dynamicComponent.id)}
		>
			<Icon icon="ph:x" />
		</button>
	</div>
{/each}
