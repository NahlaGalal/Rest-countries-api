<script lang="ts">
  import FaRegMoon from "svelte-icons/fa/FaRegMoon.svelte";
  import FaRegSun from "svelte-icons/fa/FaRegSun.svelte";

  export let toggleTheme: (name: "dark" | "light") => void;

  let theme: "light" | "dark" = "light";

  const toggleThemeHandler = () => {
    theme = theme === "dark" ? "light" : "dark";
    toggleTheme(theme);
  };
</script>

<nav>
  <h1>Where in the world?</h1>

  <button on:click={toggleThemeHandler}>
    <span>
      {#if theme === "dark"}
        <FaRegSun />
      {:else}
        <FaRegMoon />
      {/if}
    </span>
    {#if theme === "dark"}
      Light Mode
    {:else}
      Dark Mode
    {/if}
  </button>
</nav>

<style>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px 10%;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    color: var(--light-text);
    background-color: var(--light-elements);
  }

  button {
    display: flex;
    background-color: transparent;
    border: 0;
    cursor: pointer;
    gap: 8px;
    color: var(--light-text);
    align-items: center;
  }

  button:focus {
    background-color: transparent;
  }

  span {
    display: block;
    width: 16px;
    height: 16px;
  }

  @media screen and (max-width: 500px) {
    h1 {
      font-size: 1rem;
    }
  }
</style>
