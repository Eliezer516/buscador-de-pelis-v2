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
    <h1><span class="label">Titulo:</span> {data.Title}</h1>
    <h2><span class="label">Año:</span> {data.Year}</h2>
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
</style>
