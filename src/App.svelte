<script>
  import axios from "axios";
  let apikey = "9d38c929";
  let title = "";
  let movies = null;
  let error = null;
  let loading = false;

  async function searchMovies() {
    if (loading) return;
    movies = null;
    error = null;
    loading = true;
    try {
      const res = await axios.get(
        `http://www.omdbapi.com/?apikey=${apikey}&s=${title}`
      );
      console.log(res);
      movies = res.data.Search;
    } catch (err) {
      console.log(err.message);
      error = err;
    } finally {
      loading = false;
    }
  }
</script>

<input bind:value={title} />
<button on:click={searchMovies}>검색!</button>

{#if loading}
  <p style="color: royalblue">Loading...</p>
{:else if movies}
  <ul>
    {#each movies as movie}
      <li>{movie.Title}</li>
    {/each}
  </ul>
{:else if error}
  <p style="color: red;">{error.message}</p>
{/if}
