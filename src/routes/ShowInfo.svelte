<script>
  import { onMount } from 'svelte';
  onMount(async () => {
    let promise = fetch(
    "https://api.tvmaze.com/shows/1"
    ).then((x) => x.json());
  });
</script>
<h1>Show info</h1>
{#await promise}
{:then data}
  <h2>{data.name}</h2>
{:catch error}
<!-- optionally show something while promise was rejected -->
{/await}
