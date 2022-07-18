<script>
  let search = "";
  let active = false;
  import { goto } from "$app/navigation";
  import { fly, slide } from "svelte/transition";
  function cancelInactive() {
    if (search) {
      active = true;
    } else {
      active = false;
    }
  }

  function submitSearch() {
    let href = `/search/${search}`;
    goto(href);
  }
</script>

<form class="search" on:submit|preventDefault={submitSearch}>
  {#if !active}
    <label
      in:fly={{ y: -10, duration: 500 }}
      out:fly={{ y: -10, duration: 500 }}
      for="search"
    >
      Search Movies
    </label>
  {/if}

  <input
    name="search"
    type="text"
    id="search"
    on:focus={() => {
      active = true;
    }}
    class={active ? "selected" : ""}
    on:blur={cancelInactive}
    bind:value={search}
  />
  {#if search}
    <button
      out:fly={{ x: 0, duration: 200 }}
      in:fly={{ x: 50, duration: 200 }}
      type="submit">Search</button
    >
  {/if}
</form>

<style>
  .search {
    position: relative;
    width: 30%;
    min-width: 300px;
  }
  button {
    font-size: 0.7rem;
    padding: 0rem 1rem;
    background: rgb(96, 110, 223);
    font-weight: bold;
    border: none;
    color: white;
    position: absolute;
    bottom: 50%;
    right: 0;
    transform: translateY(50%);
    height: 100%;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    cursor: pointer;
  }
  label {
    position: absolute;
    top: 50%;
    left: 20px;
    color: white;
    transform: translateY(-50%);
  }
  input.selected {
    background: rgb(30, 30, 30);
  }
  input {
    width: 100%;
    border: none;
    font-size: 1rem;
    font-family: "Lato", sans-serif;
    outline: none;
    color: rgb(255, 255, 255);
    padding: 0.5rem 0.1rem;
    background: rgb(63, 63, 63);
    transition: background 0.75s ease-out;
    border-radius: 10px;
    padding: 1rem;
  }
</style>
