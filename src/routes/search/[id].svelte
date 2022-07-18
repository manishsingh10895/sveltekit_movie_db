<script context="module">
  export async function load({ fetch, params }) {
    try {
      const apiKey = import.meta.env.VITE_TMDB_API_KEY;
      let url = `https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&query=${params.id}&page=1&include_adult=false`;
      const res = await fetch(url);
      const data = await res.json();
      console.log(data);
      return {
        props: {
          movies: data.results,
        },
      };
    } catch (error) {
      console.error(error);
      return {
        props: {
          movies: [],
        },
      };
    }
  }
</script>

<script>
  import MovieCard from "../../components/MovieCard.svelte";
  export let movies;
</script>

<div class="searched-movies">
  {#each movies as movie}
    <MovieCard {movie} />
  {/each}
</div>

<style>
  .searched-movies {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    column-gap: 1rem;
    row-gap: 2rem;
  }
</style>
