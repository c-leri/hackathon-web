<script lang="ts">
    let isOpen = false;
    let selectedOption = '';

    export let moduleType: string;

    //List of possible items depending on moduleType
    let possibleItems = () => {
        switch (moduleType) {
            case ("Titre"):
                return ["Titre", "Sous-titre", "Catégorie", "Sous-catégorie", "Autre"];
                
            case ("Définition"):
                return ["Raisons", "Bon de travail", "Elément concerné", "Participants", "Autre"];

            case ("Matériel"):
                return["Matériel", "Autre"];

            case ("Etape"):
                return ["Sous-étape", "Autre"];

            case ("Résultat"):
                return ["Déficiences", "Remarques", "Autre"];
            
            case ("Signatures"):
                return ["Signature", "Autre"];
            
            default:
                return [];
        }
    }

  
    function toggleDropdown() {
      isOpen = !isOpen;
    }
  
    function selectOption(option: string) {
      selectedOption = option;
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
  {:else}
  <p>Selected Option: {selectedOption}</p> 
  {/if}
