<script>
  import { onMount } from 'svelte';
  import { Link } from 'svelte-routing';
  import Rating from '../Rating';
  let people = {
    name: 'Loading...',
    birthday: '',
    country: {
      code: '',
      name: '',
      timezone: ''
    },
    gender: '',
    image: {
      medium: ''
    },
  };

  onMount(async () => {
    const [ ,,id] = location.pathname.split('/');
    const response = await fetch(`https://api.tvmaze.com/people/${id}?embed=castcredits`)
    people = await response.json();
  });
</script>
<style>
.show-container {
  text-align:center;
  padding: 2em;
}
    .info {
      text-align: left;
    }
</style>
<div class="show-container">
<h1>{people.name}</h1>
<p><img src={people.image.medium} alt="Cover image" /></p>
<div class="info">
  <p>Birthday: {new Date(people.birthday).toDateString()} </p>
  <p>Country: {people.country.name} </p>
  <p>Gender: {people.gender} </p>
</div>
</div>
