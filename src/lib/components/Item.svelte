<script lang="ts">
    let isOpen = false;
    let selectedOption = '';
  
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
      <li on:click={() => selectOption('Option 1')}>Option 1</li>
      <li on:click={() => selectOption('Option 2')}>Option 2</li>   
      <li on:click={() => selectOption('Option 3')}>Option 3</li>
    </ul>
  {/if}
  {:else}
  <p>Selected Option: {selectedOption}</p> 
  {/if}
