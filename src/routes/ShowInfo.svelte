<script>
  import { onMount } from 'svelte';
  let show = {
    name: '',
    officialSite: '',
    genres: [],
    type: '',
    language: '',
    status: '',
    rating: '',
    premiered: '',
    image: {
      medium: ''
    }
  };

  onMount(async () => {
    const [ ,,id] = location.pathname.split('/');
    const response = await fetch(`https://api.tvmaze.com/shows/${id}`)
    show = await response.json();
  });
</script>
<style>
.show-container {
  text-align:center;
  padding: 2em;
}
</style>
<div class="show-container">
<h1>{show.name}</h1>
<p><img src={show.image.medium} alt="Cover image" /></p>
<p>Type: {show.type}</p>
<p>Language: {show.language}</p>
<p>Status: {show.status}</p>
<p>Runtime: {show.runtime}</p>

<p>Premiered: {show.premiered}</p>
<p>Rating: {show.rating}</p>

<p><a href={show.officialSite}>Website</a></p>
<p>Genres: {show.genres.join(',')}</p>
</div>
