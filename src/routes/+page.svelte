<script lang="ts">
	import Icon from '@iconify/svelte';

	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import Module from '$lib/components/Module.svelte';
	import LeftWindow from '$lib/components/LeftWindow.svelte';

	let dynamicComponents: { id: number; element: any }[] = [];
	let selectedType = '';

	function addDynamicComponent() {
		if (selectedType != '') {
			dynamicComponents = [...dynamicComponents, { id: dynamicComponents.length, element: Module }];
		}
	}

	function removeDynamicComponent(id: number) {
		dynamicComponents = [
			...dynamicComponents.filter((dynamicComponent) => dynamicComponent.id !== id)
		];
	}
</script>

<div class="grid grid-cols-4 gap-5 min-h-[100vh] py-5">
	<div class="bg-surface-600 rounded-r-lg h-full p-2 print:hidden">
		<LeftWindow bind:selectedOption={selectedType} />
	</div>
	<div
		class="h-full col-span-2 print:col-span-4 rounded-sm bg-surface-100 text-surface-900 p-5 text-center"
	>
		<AddNewModule on:click={() => addDynamicComponent()}>Ajouter un module</AddNewModule>
		{#each dynamicComponents as dynamicComponent (dynamicComponent.id)}
			{#if dynamicComponent.element === Module}
				<div
					class="border-solid border-2 border-sky-500 p-8 m-4 space-y-4 print:border-none print:p-0"
				>
					<Module moduleType={selectedType} />
				</div>
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
	</div>
	<div class="bg-surface-600 rounded-l-lg h-full p-5 print:hidden">
		Colonne 3 pour changer le style mais on a pas eu le temps :D
	</div>
</div>
