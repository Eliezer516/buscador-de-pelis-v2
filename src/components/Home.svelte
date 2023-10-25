<script>
  import InfiniteScroll from "svelte-infinite-scroll"
  import { Router, Link, Route } from "svelte-routing"
  import 'picnic/picnic.min.css'
  import Loader from './Loader.svelte'
  import { movieData } from '../store/store.js'

  let data = []
  let loader = false
  let movieToSearch = ""
  let tempSearch = ""
  let page = 1
  
  async function searchMovie() {
    page = 1
    try {
      loader = true
      const response = await fetch(`https://www.omdbapi.com/?s=${movieToSearch}&page=${page}&apikey=422350ff`)
      const json = await response.json()
      const result = json.Search
      movieData.update((n) => ([...result]))
      loader = false
      tempSearch = movieToSearch
    } catch (err) {
      console.log(err)
      loader = false
    }
  }

  async function moreMovies() {
    page++
    try {
      loader = true
      const response = await fetch(`https://www.omdbapi.com/?s=${movieToSearch}&page=${page}&apikey=422350ff`)
      const json = await response.json()
      const result = json.Search
      movieData.update((n) => ([...n, ...result]))
      loader = false
      tempSearch = movieToSearch
    } catch (err) {
      console.log(err)
      loader = false
    }
  }
</script>

<main class="container">
  <div class="title">
    <h1>Buscador de Peliculas V2.0</h1>
    <form on:submit|preventDefault={searchMovie}>
      <input bind:value={movieToSearch} type="text" placeholder="Buscar pelicula">
      <button>Buscar</button>
    </form>
  </div>
  <br/>
  <br/>
  {#if $movieData.length > 0}
    <div class="poster-container flex center two-600 three-700 four-800">
      {#each $movieData as movie}
        <Link to="{movie.imdbID}">
          <article class="card">
            <img src={movie.Poster === 'N/A' ? '/notfound.png' : movie.Poster } alt={movie.Title}>
            <footer>
              <p>{movie.Title}</p>
            </footer>
          </article>
        </Link>
      {/each}
      <InfiniteScroll threshold={100} window={true} on:loadMore={() => moreMovies()}/>
    </div>
  {/if}
  
  {#if loader}
    <Loader/>
  {/if}
</main>

<style>
  .poster-container {
    padding: 20px;
  }
  .container {
    width: 100%;
    max-width: 1240px;
    margin: 0 auto;
  }

  .title {
    width: 100%;
    text-align: center;
  }

  input {
    width: 50%;
  }

  img {
    width: 100%;
  }
</style>
