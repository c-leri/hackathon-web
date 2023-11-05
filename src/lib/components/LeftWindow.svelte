<script lang="ts">
	export let selectedOption = '';
	let selectedRadio: number | null = null;
	let headerChecked = false;
	let footerChecked = false;

	const radioButtons = [
		{ id: 1, label: 'Titre' },
		{ id: 2, label: 'Définition' },
		{ id: 3, label: 'Matériel' },
		{ id: 4, label: 'Etape' },
		{ id: 5, label: 'Résultat' },
		{ id: 6, label: 'Signatures' }
	];

	function handleRadioButtonChange(event: any) {
		selectedRadio = parseInt(event.target.value, 10);
		selectedOption = radioButtons[selectedRadio - 1].label;
	}
</script>

<div>
	<h1>Choisissez un module à ajouter</h1>

	<div class="space-y-2 my-5">
		{#each radioButtons as radioButton}
			<label class="flex items-center space-x-2">
				<input
					class="radio rounded-full"
					type="radio"
					name="radios"
					bind:group={selectedRadio}
					value={radioButton.id}
					on:change={handleRadioButtonChange}
				/>
				<p>{radioButton.label}</p>
			</label>
		{/each}

    <br>

		<label class="flex items-center space-x-2">
			<input class="checkbox" type="checkbox" bind:checked={headerChecked} />
			<p>Header</p>
		</label>
		<label class="flex items-center space-x-2">
			<input class="checkbox" type="checkbox" bind:checked={footerChecked} />
			<p>Footer</p>
		</label>
	</div>

	<button class="btn variant-outline hover:variant-filled" on:click={() => print()}>
		Imprimer
	</button>
</div>
