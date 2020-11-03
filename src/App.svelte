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

  .App {
    text-align: center;
  }
  .App code {
    background: #0002;
    padding: 4px 8px;
    border-radius: 4px;
  }
  .App p {
    margin: 0.4rem;
  }

  .App-header {
    background-color: #f9f6f6;
    color: #333;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-size: calc(10px + 2vmin);
  }
  .App-link {
    color: #ff3e00;
  }
  .App-logo {
    height: 36vmin;
    pointer-events: none;
    margin-bottom: 3rem;
    animation: App-logo-spin infinite 1.6s ease-in-out alternate;
  }
  @keyframes App-logo-spin {
    from {
      transform: scale(1);
    }
    to {
      transform: scale(1.06);
    }
  }
</style>

<Router url="{url}">
  <nav class="navbar">
    <Link to="/"><p class="navbar-link">Home</p></Link>
      <Link to="people"><p class="navbar-link">People</p></Link>
        <Link to="schedule"><p class="navbar-link">Schedule</p></Link>
          <Link to="shows"><p class="navbar-link">Shows</p></Link>
  </nav>
  <div>
    <Route path="people" component="{People}" />
    <Route path="schedule" component="{Schedule}" />
    <Route path="shows/:id" component="{ShowInfo}" />
    <Route path="shows" component="{Shows}" />
    <Route path="/"><Home /></Route>
  </div>
</Router>

