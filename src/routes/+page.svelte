<script lang="ts">
	import AddNewModule from '$lib/components/AddNewModule.svelte';
	import Module from '$lib/components/Module.svelte';

	let elements: { id: number; element: any }[] = [{ id: 0, element: AddNewModule }];

	async function addModule(index: number) {
		elements = [
			...elements.slice(0, index + 1),
			{ id: index + 1, element: Module },
			{ id: index + 2, element: AddNewModule },
			...elements
				.slice(index + 1)
				.map((element) => ({ id: element.id + 2, element: element.element }))
		];
	}
</script>

<div class="grid grid-cols-4 gap-5 min-h-[100vh] py-5">
	<div class="h-full">column 1</div>
	<div class="h-full col-span-2 rounded-sm bg-surface-100 text-surface-900 p-2 text-center">
		{#each elements as element (element.id)}
			{#if element.element === AddNewModule}
				{element.id}
				<AddNewModule on:click={() => addModule(element.id)} />
			{:else}
				{element.id}
				<svelte:component this={element.element} />
			{/if}
		{/each}
	</div>
	<div class="bg-surface-500 rounded-l-lg h-full p-2">column 3</div>
</div>
