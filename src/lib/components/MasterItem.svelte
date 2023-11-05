<script lang="ts">
    import AutreItem from "./items/AutreItem.svelte";
    import BonsItem from "./items/BonsItem.svelte";
    import CategorieItem from "./items/CategorieItem.svelte";
    import CibleItem from "./items/CibleItem.svelte";
    import DeficiencesItem from "./items/DeficiencesItem.svelte";
    import MaterielItem from "./items/MaterielItem.svelte";
    import ParticipantsItem from "./items/ParticipantsItem.svelte";
    import RaisonsItem from "./items/RaisonsItem.svelte";
    import RemarquesItem from "./items/RemarquesItem.svelte";
    import SignatureItem from "./items/SignatureItem.svelte";
    import SouscategorieItem from "./items/SouscategorieItem.svelte";
    import SousEtapeItem from "./items/SousEtapeItem.svelte";
    import SousTitreItem from "./items/SousTitreItem.svelte";


    let isOpen = false;
    let selectedOption = '';
    let filename = "";

    export let moduleType: string;

    //List of possible items depending on moduleType
    let possibleItems = () => {
        switch (moduleType) {
            case ("Titre"):
                return ["Titre", "Sous Titre", "Categorie", "Sous Categorie", "Autre"];
                
            case ("Définition"):
                return ["Raisons", "Bons", "Cible", "Participants", "Autre"];

            case ("Matériel"):
                return["Materiel", "Autre"];

            case ("Etape"):
                return ["Sous Etape", "Autre"];

            case ("Résultat"):
                return ["Deficiences", "Remarques", "Autre"];
            
            case ("Signatures"):
                return ["Signature", "Autre"];
            
            default:
                return [];
        }
    }

    const valueComponents: { [key: string]: any } = {
    AutreItem,
    BonsItem,
    CategorieItem,
    CibleItem,
    DeficiencesItem,
    MaterielItem,
    ParticipantsItem,
    RaisonsItem,
    RemarquesItem,
    SignatureItem, 
    SouscategorieItem,
    SousEtapeItem,
    SousTitreItem,
  };

    function getItemFileName(item: string){
        return item.trim() + "Item";
    }
  
    function toggleDropdown() {
      isOpen = !isOpen;
    }
  
    function selectOption(option: string) {
      selectedOption = option;
        filename = getItemFileName(selectedOption);
    }


  </script>
  
{#if !selectedOption} 
    {#if isOpen}
        <button class="btn-xl" on:click={toggleDropdown}>Annuler</button>
        {#each possibleItems() as item (item)}
            <button class="btn-xl" on:click={() => selectOption(item)}>{item}</button>
        {/each}
    {:else}
    <button class="btn-xl" on:click={toggleDropdown}>Sélectionner un élément</button>
    {/if}
{:else if filename in valueComponents}
    {#await valueComponents[filename]}
        Loading...
        {:then component}
        {#if component}
            <svelte:component this={component} />
        {:else}
            Component not found
        {/if}
    {/await}
{:else}
<p>Default content for unknown value</p>
{/if}