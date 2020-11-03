<script>
import { onMount } from 'svelte';
 import {  Link } from "svelte-routing";

let shows = [];

let countries = [
  { id: 1, text: 'US', value: 'US' },
  { id: 2, text: 'India', value: 'IN' },
  { id: 3, text: 'United Kingdom', value: 'GB' },
  { id: 4, text: 'Malaysia', value: 'MY' },
  { id: 5, text: 'Mexico', value: 'MX' },
  { id: 6, text: 'Nepal', value: 'NP' },
  { id: 7, text: 'Netherlands', value: 'NL' },
  { id: 8, text: 'Australia', value: 'AU' },
  { id: 9, text: 'Hong Kong', value: 'HK' },
  { id: 10, text: 'Japan', value: 'JP' },
];

let selected = countries[0];
let selectedDate;
let country;
  const date = new Date().toISOString().split('T')[0];
onMount(async () => {
  const response = await fetch(`https://api.tvmaze.com/schedule`);
shows = await response.json();
});

async function getSchedule() {

  console.log(selectedDate);
  const response = await fetch(`https://api.tvmaze.com/schedule?country=${selected.value}&date=${selectedDate}`);
shows = await response.json();
}
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
<h1>Schedule</h1>
<p>Country:
<select bind:value={selected} on:change="{getSchedule}">
		{#each countries as country}
			<option value={country}>
				{country.text}
			</option>
		{/each}
	</select>
</p>
<p>Date: <input type="date" bind:value={selectedDate} on:change="{getSchedule}"/></p>
<ul>
{#each shows as { airtime, name, show }, i}
<li>
  <p><Link to="shows/{show.id}">{name}</Link></p>
<img src={show.image.medium}/>
<p>Airtime: {airtime}</p>
<p>Runtime: {show.runtime} minutes</p>
<p>Network: {show.network && show.network.name}</p>
</li>
{/each}
</ul>

