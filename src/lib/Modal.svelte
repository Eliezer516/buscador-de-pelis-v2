<script>
  import {movieData} from '../store/store.js'
</script>

<div class="modal">
  <input id="modal_1" type="checkbox" />
  <label for="modal_1" class="overlay"></label>
  <article class="card">
    <header class="img-container">
      <label for="modal_1" class="close">&times;</label>
      <img src={$movieData.Poster === 'N/A' ? '/notfound.png' : $movieData.Poster} alt={$movieData.Title}>
    </header>
    <footer>
      <h1>Titulo: {$movieData.Title}</h1>  
      <h2>Tipo: {#if $movieData.Type === 'movie'}Pelicula {:else if $movieData.Type === 'series'}Serie{/if}</h2>
      <h2>Año: {$movieData.Year}</h2>
    </footer>
  </article>
</div>

<style>
  .img-container {
    display: grid;
    place-items: center;
  }

  footer {
    text-align: center;
  }
</style>
