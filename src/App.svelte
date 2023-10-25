<script>
  import { Router, Link, Route } from "svelte-routing"
  import Home from './components/Home.svelte'
  import Movie from './components/Movie.svelte'

  export let url = "";
  let basepath = "/buscador-de-pelis-v2"
</script>

<Router {url} {basepath}>
  <Route path="/"><Home /></Route>
  <Route path="/:id" let:params><Movie id={params.id} /></Route>
</Router>
