<script>
  import { onMount } from "svelte";

  export let params;

  onMount(() => console.log(params));
</script>

<div class="container">This is a news app created with Svelte</div>

<style>
</style>
