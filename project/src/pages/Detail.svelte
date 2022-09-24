<script type="ts">
  import { onMount } from "svelte";
  import IoIosArrowRoundBack from "svelte-icons/io/IoIosArrowRoundBack.svelte";
  import { navigate } from "svelte-routing";
  export let name: string;

  const getCountryHandler = async () => {
    let country: {
      borders: string[];
      capital: string[];
      currencies: { [key: string]: { name: string; symbol: string } };
      flags: { png: string; svg: string };
      languages: { [key: string]: string };
      name: {
        common: string;
        official: string;
        nativeName: { [key: string]: string };
      };
      population: number;
      region: string;
      subregion: string;
      tld: string[];
    };

    const res = await fetch(
      `https://restcountries.com/v3.1/name/${name}?fields=flags,name,population,region,subregion,capital,tld,currencies,languages,borders`
    );
    const data = await res.json();

    if (!data.status) {
      country = data[0];
    } else {
      throw new Error("No country with this name");
    }

    return country;
  };

  let promise: any = getCountryHandler();

  onMount(async () => {
    promise = await getCountryHandler();
  });

  const navigateToHome = () => navigate("/");
</script>

<div class="container">
  <header>
    <button class="back-btn" on:click={navigateToHome}>
      <span>
        <IoIosArrowRoundBack />
      </span>
      Back
    </button>
  </header>

  <main>
    {#await promise}
      <p>Loading...</p>
    {:then country}
      <div class="country-container">
        <img class="flag" src={country.flags.png} alt="The flag of {name}" />

        <section>
          <h2>{name}</h2>

          <div class="country-data">
            <dl>
              <div class="country-data__item">
                <dt>Native name:</dt>
                <dd>
                  {country.name.nativeName[
                    Object.keys(country.name.nativeName)[0]
                  ].common}
                </dd>
              </div>
              <div class="country-data__item">
                <dt>Population:</dt>
                <dd>
                  {new Intl.NumberFormat("en-US").format(country.population)}
                </dd>
              </div>
              <div class="country-data__item">
                <dt>Region:</dt>
                <dd>{country.region}</dd>
              </div>
              <div class="country-data__item">
                <dt>Sub region:</dt>
                <dd>{country.subregion}</dd>
              </div>
              <div class="country-data__item">
                <dt>Capital:</dt>
                <dd>{country.capital.join(", ")}</dd>
              </div>
            </dl>

            <dl>
              <div class="country-data__item">
                <dt>Top Level Domain:</dt>
                <dd>{country.tld.join(", ")}</dd>
              </div>
              <div class="country-data__item">
                <dt>Currencies:</dt>
                <dd>
                  {Object.values(country.currencies)
                    .map((cur) => cur.name)
                    .join(", ")}
                </dd>
              </div>
              <div class="country-data__item">
                <dt>Languages:</dt>
                <dd>{Object.values(country.languages).join(", ")}</dd>
              </div>
            </dl>
          </div>

          <dl>
            <div class="country-borders">
              <dt>Border Countries:</dt>
              <dd>
                {#each country.borders as border (border)}
                  <span>{border}</span>
                {/each}
              </dd>
            </div>
          </dl>
        </section>
      </div>
    {:catch error}
      <p>{error.message}</p>
    {/await}
  </main>
</div>

<style>
  .country-container {
    display: flex;
    gap: 40px;
    align-items: center;
    flex-wrap: wrap;
    justify-content: space-between;
    color: var(--light-text);
  }

  .back-btn {
    color: var(--light-text);
    background: var(--light-elements);
    padding: 4px 24px;
    border-radius: 5px;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    display: flex;
    align-items: center;
    gap: 8px;
    cursor: pointer;
    margin-bottom: 40px;
  }

  .back-btn span {
    display: block;
    width: 16px;
    height: 16px;
    color: var(--light-text);
  }

  .flag {
    max-width: 100%;
  }

  section {
    flex: 1;
  }

  h2 {
    margin-bottom: 24px;
  }

  .country-data {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 24px;
  }

  .country-data__item {
    display: flex;
    gap: 8px;
  }

  .country-data__item dt,
  .country-borders dt {
    font-weight: 600;
  }

  .country-borders {
    display: flex;
    gap: 8px;
    margin-top: 40px;
    align-items: center;
    flex-wrap: wrap;
  }

  .country-borders dd {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .country-borders span {
    background: var(--light-elements);
    padding: 4px 24px;
    border-radius: 5px;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
  }
</style>
