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
    { id: 6, label: 'Signatures' },
  ];

        
        function handleRadioButtonChange(event: any) {
    selectedRadio = parseInt(event.target.value, 10);
    selectedOption = radioButtons[selectedRadio-1].label;
  }

</script>

<div>
    <h1>Choisissez un module à ajouter</h1>

    {#each radioButtons as radioButton}
  <label>
    <input
      type="radio"
      name="radios"
      bind:group={selectedRadio}
      value={radioButton.id}
      on:change={handleRadioButtonChange}
    />
    {radioButton.label}
  </label>
{/each}

    <label>
        <input type="checkbox" bind:checked={headerChecked} />
        Header
      </label>
      <label>
        <input type="checkbox" bind:checked={footerChecked} />
        Footer
      </label>
</div>