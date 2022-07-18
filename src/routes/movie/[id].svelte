<script context="module">
  export async function load({ fetch, params }) {
    try {
      let apiKey = import.meta.env.VITE_TMDB_API_KEY;
      let id = params.id;
      let url = `https://api.themoviedb.org/3/movie/${id}?api_key=${apiKey}`;

      const res = await fetch(url);
      const data = await res.json();
      console.log(data);
      if (res.ok) {
        return {
          props: {
            movie: data,
          },
        };
      } else {
        return {
          props: {
            movie: {},
          },
        };
      }
    } catch (error) {}
  }
</script>

<script>
  export let movie;
  import { fly } from "svelte/transition";
</script>

<div
  class="movie-details"
  in:fly={{ y: 50, delay: 500, duration: 250 }}
  out:fly={{ duration: 250 }}
>
  <div class="img-container">
    <img
      src={`https://image.tmdb.org/t/p/original/${movie.backdrop_path}`}
      alt={movie.title}
    />
  </div>

  <div class="txt-container">
    <h1>
      {movie.title}
    </h1>
    <p class="overview">
      {movie.overview}
    </p>
    <p>
      <span> Release Date </span>
      {movie.release_date} <br />
      <span> Budget: </span>
      {movie.budget} <br />

      <span>Rating: </span>
      {movie.vote_average} <br />

      <span>Runtime:</span>
      {movie.runtime}mins <br />
    </p>
  </div>
</div>

<style>
  h1 {
    padding: 1rem 0rem 2rem;
  }

  p {
    padding: 1rem 0rem;
  }

  .img-container {
    width: 100%;
  }

  img {
    width: 100%;
    border-radius: 1rem;
  }

  .movie-details {
    margin: 2rem 20%;
  }

  span {
    font-weight: bold;
  }
</style>
