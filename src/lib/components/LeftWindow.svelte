<script lang="ts">

export let selectedOption = '';

    const ModuleTypes: string[] = [
        "Titre",
        "Définition",
        "Matériel",
        "Etape",
        "Résultat",
        "Signatures"
    ];

    function selectOption(option: string) {
      selectedOption = option;
        }    

</script>

<div>
    <h1>Choisissez un module à ajouter</h1>
    {#each ModuleTypes as moduleType (moduleType)}
          <button class="variant-outline-surface w-full hover:variant-filled-surface" on:click={() => selectOption(moduleType)}>{moduleType}</button>
    {/each}
</div>