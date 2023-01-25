<template>

  <div class="container">
    <div class="row justify-content-left">
      <div class="col-lg-4 col-md-8 col-sm-10">

        <div class="single-feature">
          <div class="icon">
            <font-awesome-icon icon="fa-solid fa-cocktail" />
          </div>
          <div class="content">

            <div>
              <h1 class="">{{ cocktail.strDrink }}</h1>

            </div>
          </div>

        </div>
      </div>
      <div class="col-lg-4 col-md-8 col-sm-10">
        <div class="single-feature">
          <div class="icon">
            <font-awesome-icon icon="fa-solid fa-list" />
          </div>
          <div class="content">
            <p>

            <h2>How to make it:</h2>
            <p class="wow fadeInUp" data-wow-delay=".9s">{{ cocktail.strInstructions }}</p>

            </p>
            <br>
            
            <div v-if="cocktail.strVideo != null">
              <p ><h2>Video tutorial:</h2><a :href="cocktail.strVideo">{{ cocktail.strVideo }}</a></p>
          </div>
          </div>
        </div>
      </div>
      <div class="col-lg-4 col-md-8 col-sm-10">
        <div class="single-feature">
          <div class="icon">
            <font-awesome-icon icon="fa-solid fa-lemon" />
          </div>
          <div class="content">

            <p>

            <h2>What you need:</h2>

            <ol type="1" class="text-white text-center wow fadeInUp" data-wow-delay=".4s"
              v-for="ingredient in ingredientList">
              <li v-if="ingredient.ingredient != null">{{ ingredient.ingredient }} - <h6 class="text-blue">{{
                ingredient.measure
              }}</h6>
              </li>

            </ol>
            </p>

          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  props: {
    cocktail: {
      required: true
    },
    ingredientList: null

  }
}
</script>



