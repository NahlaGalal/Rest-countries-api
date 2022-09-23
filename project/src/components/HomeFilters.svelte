<script type="ts">
  import IoIosSearch from "svelte-icons/io/IoIosSearch.svelte";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  const regions = ["Africa", "Americas", "Asia", "Europe", "Oceania"];

  let searchVal: string = "";
  let region: string = "";
  let timer: any;

  const onSearchHandler = () => {
    clearTimeout(timer);
    timer = setTimeout(() => {
      dispatch("search", {
        searchVal,
      });
    }, 300);
  };

  const onFilterRegion = () => {
    dispatch("filter", { region });
  };
</script>

<header class="header">
  <!-- Search input -->
  <div class="search">
    <input
      class="input"
      type="search"
      placeholder="Search for a country..."
      bind:value={searchVal}
      on:input={onSearchHandler}
    />

    <div class="search__icon"><IoIosSearch /></div>
  </div>

  <!-- Select filter -->
  <select bind:value={region} class="input select" on:change={onFilterRegion}>
    <option value="" disabled>Filter by Region</option>
    {#each regions as region}
      <option value={region}>
        {region}
      </option>
    {/each}
  </select>
</header>

<style>
  .header {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    gap: 16px;
    margin-bottom: 40px;
  }

  .search {
    position: relative;
    max-width: 300px;
    width: 100%;
  }

  .input {
    height: 40px;
    width: 100%;
    padding: 8px 16px 8px 40px;
    border: 0;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    border-radius: 5px;
    font-size: 14px;
    background-color: var(--light-elements);
    color: var(--light-text);
    outline: transparent;
  }

  .search__icon {
    position: absolute;
    width: 16px;
    height: 16px;
    left: 16px;
    top: 50%;
    transform: translateY(-50%);
  }

  .select {
    max-width: 150px;
    padding: 8px 16px;
  }
</style>
