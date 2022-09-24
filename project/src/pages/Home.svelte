<script type="ts">
  import { onMount } from "svelte";
  import CountryCard from "../components/CountryCard.svelte";
  import HomeFilters from "../components/HomeFilters.svelte";

  let countries: {
    img: string;
    name: string;
    population: number;
    region: string;
    capital: string;
  }[] = [];

  const getCountries = async (url: string) => {
    const res = await fetch(`https://restcountries.com/v3.1/${url}`);
    const data = await res.json();

    if (data.status === 404) countries = [];

    countries = data.map((country: any) => ({
      img: country.flags.png,
      name: country.name.common,
      population: country.population,
      region: country.region,
      capital: country.capital?.join(", "),
    }));
  };

  onMount(async () => {
    getCountries("all");
  });

  const onSearchHandler = async (e) => {
    const { searchVal } = e.detail;
    getCountries(searchVal ? `name/${searchVal}` : "all");
  };

  const onFilterRegion = async (e) => {
    const { region } = e.detail;
    getCountries(`region/${region}`);
  };
</script>

<div class="container">
  <HomeFilters on:search={onSearchHandler} on:filter={onFilterRegion} />

  <main class="cards">
    <!-- Cards -->
    {#each countries as country}
      <CountryCard {country} />
    {:else}
      <p>Loading...</p>
    {/each}
  </main>
</div>

<style>
  .cards {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 24px;
  }

  @media screen and (max-width: 1200px) {
    .cards {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  @media screen and (max-width: 800px) {
    .cards {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media screen and (max-width: 520px) {
    .cards {
      grid-template-columns: 1fr;
    }
  }
</style>
