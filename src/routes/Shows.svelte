<script>
import { onMount } from 'svelte';
 import {  Link } from "svelte-routing";

let shows = [];
onMount(async () => {
const response = await fetch('https://api.tvmaze.com/shows');
shows = await response.json();
});
</script>

<style>
ul {
display:flex;
flex-wrap: wrap;
}

li {
margin: 1em;
padding: 1em;
border: 1px solid black;
list-style: none;
text-align: center;
}
</style>
<h1>Shows Page</h1>
<ul>
{#each shows as { id, name, image }, i}
<li>
  <Link to="shows/{id}">{name}</Link>
<img src={image.medium}/>
</li>
{/each}
</ul>

