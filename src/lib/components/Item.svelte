<script lang="ts">
    let isOpen = false;
    let selectedOption = '';

    export let moduleType: string;

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
      isOpen = false;
    }
  </script>
  
  {#if !selectedOption}
    

  <button on:click={toggleDropdown}>Toggle Dropdown</button>
  
  {#if isOpen}
    {#each possibleItems() as item (item)}
    <button on:click={() => selectOption(item)}>{item}</button>
    {/each}
  {/if}
  {:else}
  <p>Selected Option: {selectedOption}</p> 
  {/if}
