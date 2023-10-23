<script>
  import 'picnic/picnic.min.css'
  import Modal from './lib/Modal.svelte'
  import Loader from './lib/Loader.svelte'
  import {movieData} from './store/store.js'

  let data = []
  let loader = false
  let movieToSearch = ""
  
  async function searchMovie() {
    try {
      loader = true
      const response = await fetch(`https://www.omdbapi.com/?s=${movieToSearch}&apikey=422350ff`)
      const json = await response.json()
      data = json.Search || []
      loader = false
    } catch (err) {
      console.log(err)
      loader = false
    }
  }

  function updateMovieData(movie) {
    movieData.update((n) => ({...movie}))
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
  {#if data.length > 0}
    <div class="poster-container flex center two-600 three-700 four-800">
      {#each data as movie}
        <label for="modal_1" on:click={updateMovieData(movie)}>
          <img src={movie.Poster || "/notfound.png"} alt={movie.Title}>
        </label>
      {/each}
    </div>
  {/if}
  
  {#if loader}
    <Loader/>
  {/if}
  
  <Modal/>
</main>

<style>
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
