<script>
  import {movieData} from '../store/store.js'
</script>

<div class="modal">
  <input id="modal_1" type="checkbox" />
  <label for="modal_1" class="overlay"></label>
  <article class="card">
    <img src={$movieData.Poster || "/notfound.png"} alt={$movieData.Title}>
    <footer>
      <h1>Titulo: {$movieData.Title}</h1>  
      <h2>Tipo: {#if $movieData.Type === 'movie'}Pelicula {:else if $movieData.Type === 'series'}Serie{/if}</h2>
      <h2>Año: {$movieData.Year}</h2>
    </footer>
  </article>
</div>

<style>
  img {
    margin: 0 auto;
  }

  footer {
    text-align: center;
  }
</style>
