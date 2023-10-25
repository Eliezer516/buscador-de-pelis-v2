<script>
  import {onMount} from 'svelte'
  import Loader from './Loader.svelte'
  export let id

  let data
  
  async function movieDetails() {
    try {
      const response = await fetch(`https://www.omdbapi.com/?i=${id}&plot=full&apikey=422350ff`)
      const json = await response.json()
      data = json
      console.log(data)
    } catch (err) {
      console.log(err)
    }
  }

  onMount(() => {
    movieDetails()
  })
</script>

  {#if data}
<section>
  <aside>
    <img src={data.Poster === 'N/A' ? '/notfound.png' : data.Poster } alt={data.Title}>
  </aside>
  <div>
    <h2><span class="strong">Titulo:</span> {data.Title}</h2>
    <p><span class="strong">Año:</span> {data.Year}</p>
    <p><span class="strong">Tipo:</span> {data.Type}</p>
    <p><span class="strong">Director:</span> {data.Director}</p>
    <p><span class="strong">Actores:</span> {data.Actors}</p>
    <p><span class="strong">Idioma original:</span> {data.Language}</p>
    <p><span class="strong">Lugar de grabación:</span> {data.Country}</p>
    <p><span class="strong">IMDb Rating:</span> {data.imdbRating}</p>
    <p><span class="strong">Trama:</span> {data.Plot}</p>
  </div>
</section>
  {:else}
    <Loader />
  {/if}

<style>
  section {
    display: flex;
    gap: 20px;
    padding: 20px;
  }

  img {
    position: sticky;
    top: 20px;
  }

  .strong {
    font-weight: bold;
  }

  @media screen and (max-width: 650px) {
    section {
      flex-direction: column;
    }

    aside {
      display: grid;
      place-items: center;
    }
  }
</style>
