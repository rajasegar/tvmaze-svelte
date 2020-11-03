<script>
  export let rating;
  $: _rating = Math.round(rating);
  $: unrated = 10 - _rating;
</script>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
<style>
  .checked {
    color: orange;
  }
</style>
{#each Array(_rating) as _, row}
<span class="fa fa-star checked"></span>
{/each}
{#each Array(unrated) as _, row}
<span class="fa fa-star"></span>
{/each}
