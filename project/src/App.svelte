<script lang="ts">
  import { Router, Route } from "svelte-routing";
  import Navbar from "./components/Navbar.svelte";
  import Home from "./pages/Home.svelte";
  import Detail from "./pages/Detail.svelte";

  document.title = "Rest countries Api"

  const toggleTheme = (name: "dark" | "light") => {
    if(name === "dark") {
      document.documentElement.style.setProperty('--light-text', 'hsl(0, 0%, 100%)');
      document.documentElement.style.setProperty('--light-elements', 'hsl(209, 23%, 22%)');
      document.documentElement.style.setProperty('--light-background', 'hsl(207, 26%, 17%)');
    } else {
      document.documentElement.style.setProperty('--light-text', 'hsl(200, 15%, 8%)');
      document.documentElement.style.setProperty('--light-elements', 'hsl(0, 0%, 100%)');
      document.documentElement.style.setProperty('--light-background', 'hsl(0, 0%, 98%)');
    }
  };

  export let url = "";
</script>

<Navbar {toggleTheme} />
<Router {url}>
  <Route path="/" component={Home} />
  <Route path="/detail/:name" let:params>
    <Detail name={params.name} />
  </Route>
</Router>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@300;600;800&display=swap");

  :global(:root) {
    --light-text: hsl(200, 15%, 8%);
    --light-elements: hsl(0, 0%, 100%);
    --light-background: hsl(0, 0%, 98%);
    --light-input: hsl(0, 0%, 52%);
  }

  :global(body) {
    margin: 0;
    padding: 0;
    font-family: "Nunito Sans";
    background-color: var(--light-background);
  }

  :global(*, button, input, select, textarea) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(.container) {
    padding: 40px 10%;
  }
</style>
