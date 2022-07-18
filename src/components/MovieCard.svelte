<script>
  export let movie;
</script>

<div class="movie-card">
  <a sveltekit:noscroll sveltekit:prefetch href={`/movie/${movie.id}`}>
    <img
      src={`https://image.tmdb.org/t/p/w500` + movie.poster_path}
      alt={movie.title}
    />
  </a>
  <div class="description">
    <h2>{movie.title}</h2>
    <p>
      {movie.release_date}
    </p>
  </div>
</div>

<style>
  img {
    width: 100%;
    object-fit: cover;
    height: 30vh;
    min-height: 250px;
    border-top-left-radius: 16px;
    border-top-right-radius: 16px;
  }

  .movie-card {
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    padding: 1rem;
  }

  .description {
    padding: 0.1rem 1rem;
  }
  p {
    font-size: 0.7rem;
  }
</style>
