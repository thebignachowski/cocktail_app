<script lang="ts">
  import { fade } from "svelte/types/runtime/transition";

  export let drinkData: Array<any>;
</script>

<div class="card mx-2 my-2 elemento" style="width: 18rem;">
  <img
    loading="lazy"
    src={drinkData.strDrinkThumb}
    class="card-img-top mt-2"
    alt={drinkData.idDrink}
  />
  <div class="card-body">
    <h5 class="card-title">{drinkData.strDrink}</h5>
    <p class="card-text">
      {drinkData.strInstructions}
    </p>
  </div>
</div>

<style>
  .card-text {
    height: 15rem;
  }
</style>
