<script>
 import { Router, Link, Route } from "svelte-routing";
  import Home from "./routes/Home.svelte";
  import People from "./routes/People.svelte";
  import Schedule from "./routes/Schedule.svelte";
  import Shows from "./routes/Shows.svelte";
  import ShowInfo from "./routes/ShowInfo.svelte";

  export let url = "";

</script>

<style>
  :global(body) {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
  }

  .navbar {
    display: flex;
    background: #000;
  }

  .navbar-link  {
    padding: 1em;
    color: #fff;
    text-decoration: none;
    margin:0;
  }

  .navbar-link:hover {
    text-decoration: underline;
    background: blueviolet;
  }


</style>

<Router url="{url}">
  <nav class="navbar">
    <Link to="/"><p class="navbar-link">Home</p></Link>
        <Link to="schedule"><p class="navbar-link">Schedule</p></Link>
          <Link to="shows"><p class="navbar-link">Shows</p></Link>
  </nav>
  <div>
    <Route path="people/:id" component="{People}" />
    <Route path="schedule" component="{Schedule}" />
    <Route path="shows/:id" component="{ShowInfo}" />
    <Route path="shows" component="{Shows}" />
    <Route path="/"><Home /></Route>
  </div>
</Router>

