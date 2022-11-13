<script lang="ts">
  import axios from "axios";
  import Cocktail from "./Cocktail.svelte";
  import { fade } from "svelte/types/runtime/transition";

  let drinks: Array<any> = [];
  let drinkName: string = "";

  const getDrinks = async (drinkSearch: string = "margarita") => {
    const { data } = await axios.get(
      `https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${drinkSearch}`
    );

    drinks = data.drinks;
  };

  let promise = getDrinks();

  const handleSubmit = () => {
    promise = getDrinks(drinkName);
  };
</script>

<div class="container text-center mt-3">
  <h2>Search Cocktail</h2>
  <form on:submit|preventDefault={handleSubmit} class="d-flex">
    <input bind:value={drinkName} type="text" class="form-control mx-2" />
    <button type="submit" class="btn btn-info mt-2">Search</button>
  </form>
  {#await promise}
    <div class="spinner-grow" style="width: 3rem; height: 3rem;" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  {:then drinksResponse}
    <div class="row galeria">
      {#each drinks as drink}
        <Cocktail drinkData={drink} />
      {/each}
    </div>
  {/await}
</div>

<style>
  .galeria {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  @media (min-width: 768px) {
    .galeria {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1rem;
      align-items: flex-start;
      justify-content: space-around;
      height: 30rem;
    }
  }
</style>
