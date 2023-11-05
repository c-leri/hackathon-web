<script lang="ts">
	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import Module from '$lib/components/Module.svelte';
	import LeftWindow from '$lib/components/LeftWindow.svelte';

	let dynamicComponents: any[] = [AddNewModule];
	let selectedType = '';

	async function addDynamicComponent() {
		if (selectedType != '') {
			dynamicComponents = [...dynamicComponents, Module];
		}
	}
</script>

<div class="grid grid-cols-4 gap-5 min-h-[100vh] py-5">
	<div class="h-full print:hidden"><LeftWindow bind:selectedOption={selectedType} /></div>
	<div class="h-full col-span-2 print:col-span-4 rounded-sm bg-surface-100 text-surface-900 p-2 text-center">
		{#each dynamicComponents as element}
			{#if element === AddNewModule}
				<AddNewModule on:click={() => addDynamicComponent()}>Ajouter un module</AddNewModule>
			{:else if element === Module}
				<div class="border-solid border-2 border-sky-500 p-8 m-4 space-y-4">
					<Module moduleType={selectedType} />
				</div>
			{:else}
				<svelte:component this={element} />
			{/if}
		{/each}
	</div>
	<div class="bg-surface-500 rounded-l-lg h-full p-2 print:hidden">
		Colonne 3 pour changer le style mais on a pas eu le temps :D
	</div>
</div>
