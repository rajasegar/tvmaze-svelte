<script>
  import { onMount } from 'svelte';
  import { Link } from 'svelte-routing';
  import Rating from '../Rating';
  let show = {
    name: 'Loading...',
    officialSite: '',
    genres: [],
    type: '',
    language: '',
    status: '',
    rating: {
      average: 0,
    },
    premiered: '',
    image: {
      medium: ''
    },
    _embedded: {
      cast: []
    }
  };

  onMount(async () => {
    const [ ,,id] = location.pathname.split('/');
    const response = await fetch(`https://api.tvmaze.com/shows/${id}?embed=cast`)
    show = await response.json();
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
<h1>{show.name}</h1>
<p><img src={show.image.medium} alt="Cover image" /></p>
<div class="info">
<p>Type: {show.type}</p>
<p>Language: {show.language}</p>
<p>Status: {show.status}</p>
<p>Runtime: {show.runtime} minutes</p>

<p>Premiered: {new Date(show.premiered).toDateString()}</p>
<p>Rating: {show.rating.average} <Rating rating={show.rating.average} /></p>

<p><a target="_blank" href={show.officialSite}>Website</a></p>
<p>Genres: {show.genres.join(',')}</p>
<p>Cast: 
{#each show._embedded.cast as cast }
  <Link to="people/{cast.person.id}"><span>{cast.person.name}, </span></Link>
{/each}
</p>
</div>
</div>
