<script type="ts">
  import { link } from "svelte-routing";

  export let country: {
    img: string;
    name: string;
    population: number;
    region: string;
    capital: string;
  } = {
    img: "",
    name: "",
    population: 0,
    region: "",
    capital: "",
  };
</script>

<section>
  <a class="link" href={`/detail/${country.name}`} use:link>
    <img src={country.img} alt="" />
    <p class="name">{country.name}</p>
    <p>
      <span>Population: </span>
      {new Intl.NumberFormat("en-US").format(country.population)}
    </p>
    <p><span>Region: </span> {country.region}</p>
    <p><span>Capital: </span> {country.capital}</p>
  </a>
</section>

<style>
  section {
    background-color: var(--light-elements);
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    color: var(--light-text);
    padding-bottom: 40px;
  }

  .link {
    color: var(--light-text);
    text-decoration: none;
  }

  img {
    width: 100%;
    height: 150px;
  }

  .name {
    font-weight: 800;
    padding: 16px;
  }

  p {
    padding-left: 16px;
  }

  p span {
    font-weight: 600;
  }
</style>
