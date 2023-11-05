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
	const colors = [
		'bg-surface-50',
		'bg-red-50',
		'bg-green-50',
		'bg-blue-50',
		'bg-pink-50',
		'bg-primary-50'
	];
	let selected = colors[0];
</script>

<div class="grid grid-cols-4 gap-5 min-h-[100vh] py-5">
	<div class="h-full print:hidden"><LeftWindow bind:selectedOption={selectedType} /></div>
	<div
		class="h-full col-span-2 print:col-span-4 rounded-sm {selected} text-surface-900 p-2 text-center"
	>
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
	<div class=" rounded-l-lg h-full p-2 print:hidden">
		Choississez une couleur de fond : 
		<div class="grid grid-cols-6 gap-3">
			{#each colors as color, i}
				<button
					aria-current={selected === color}
					class={`aspect-square rounded-full color-picker text-surface-800 ${color}`}
					on:click={() => (selected = color)}
				>
					{i + 1}
				</button>
			{/each}
		</div>
	</div>
</div>

<style>
	.color-picker {
		transform: translate(-2px, -2px);
		filter: drop-shadow(2px 2px 3px rgba(0, 0, 0, 0.2));
		transition: all 0.1s;
	}

	.color-picker[aria-current='true'] {
		transform: none;
		filter: none;
		box-shadow: inset 3px 3px 4px rgba(0, 0, 0, 0.2);
	}
</style>
