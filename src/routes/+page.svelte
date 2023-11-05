<script lang="ts">
	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import Module from '$lib/components/Module.svelte';
	import TitleModule from '$lib/components/TitleModule.svelte';

	let dynamicComponents: any[] = [AddNewModule];

async function addDynamicComponent(index: number) {
  dynamicComponents = [
	...dynamicComponents.slice(0, index + 1),
	Module,
	...dynamicComponents.slice(index + 1),
  ];
}
</script>

<div class="grid grid-cols-4 gap-5 min-h-[100vh] py-5">
	<div class="h-full">column 1</div>
	<div class="h-full col-span-2 rounded-sm bg-surface-100 text-surface-900 p-2 text-center">
		{#each dynamicComponents as element, index (index)}
			{#if element === AddNewModule}
				{index}
				<AddNewModule on:click={() => addDynamicComponent(index)}>Ajouter un module</AddNewModule>
			{:else}
				{index}
				<svelte:component this={element} />
			{/if}
		{/each}
	</div>
	<div class="bg-surface-500 rounded-l-lg h-full p-2">column 3</div>
</div>
