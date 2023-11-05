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
    <ul>
      <li> <button on:click={() => selectOption('Option 1')}>Option 1</button></li>
      <li> <button on:click={() => selectOption('Option 2')}>Option 2</button></li>   
      <li> <button on:click={() => selectOption('Option 3')}>Option 3</button></li>
    </ul>
  {/if}
  {:else}
  <p>Selected Option: {selectedOption}</p> 
  {/if}
