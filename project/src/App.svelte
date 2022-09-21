<script lang="ts">
  import Navbar from "./Navbar.svelte";
</script>

<Navbar />

<style>
  @import url("https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@300;600;800&display=swap");
	
  :global(:root) {
    --dark-text: hsl(0, 0%, 100%);
    --dark-elements: hsl(209, 23%, 22%);
    --dark-background: hsl(207, 26%, 17%);
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
</style>
