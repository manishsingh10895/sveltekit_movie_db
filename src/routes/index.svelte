<script context="module">
  export async function load({ fetch }) {
    const apiKey = import.meta.env.VITE_TMDB_API_KEY;
    const url = `https://api.themoviedb.org/3/movie/popular?api_key=${apiKey}&language=en-US&page=1`;

    const res = await fetch(url);

    const data = await res.json();
    console.log(data);
    if (res.ok) {
      return {
        props: {
          popular: data.results,
        },
      };
    } else {
      return {
        props: {
          popular: [],
        },
      };
    }
  }
</script>

<script>
  import PopularMovies from "../components/PopularMovies.svelte";
  import SearchMovies from "../components/SearchMovies.svelte";
  export let popular;
  import "../global.css";
  import { fly } from "svelte/transition";
</script>

<section
  in:fly={{ y: 50, duration: 250, delay: 250 }}
  out:fly={{ duration: 250 }}
>
  <SearchMovies />
  <PopularMovies {popular} />
</section>
