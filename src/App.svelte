<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import Counter from "./lib/Counter.svelte";
  import List from "./lib/list.svelte";
</script>

<h1>Matcher</h1>
<main>
  <List />
  <List />
</main>

<style>
  main {
    display: grid;
    grid: 100% / auto auto;
    column-gap: 4em;
  }
</style>
