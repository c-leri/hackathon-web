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
      console.log(option);
    }    

</script>

<div>
    {#each ModuleTypes as moduleType (moduleType)}
    {console.log(moduleType)}
      <button class="variant-outline-surface w-full hover:variant-filled-surface" on:click={() => selectOption(moduleType)}>{moduleType}</button>
    {/each}
</div>