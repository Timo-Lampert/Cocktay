<template>
  <div v-if="this.cocktail != null">

    <v-card class="mx-auto  justify-center wavebg" >
      <a href="#features" @click="this.$emit('cocktailItem', this.cocktail,ingredientList)">
      <div class="waves "></div>
      <div class="waves "></div>
      <div class="waves "></div>
      <v-img v-if="this.cocktail.strDrinkThumb != null" v-bind:src="this.cocktail.strDrinkThumb" width="220" cover  ></v-img>

      <v-card-title class="text-center">
        <h6 class="text-dark">{{ this.cocktail.strDrink.toUpperCase().substring(0, 18) }}</h6>
      </v-card-title>

      <v-card-subtitle>

        {{ this.cocktail.strIngredient1 }}
        ,
        {{ this.cocktail.strIngredient2 }}
        <br>
        {{ this.cocktail.strIngredient3 }}




      </v-card-subtitle>
    </a>
      <v-card-actions>
        <v-btn color="orange-lighten-2" variant="text">
          {{cocktail.strAlcoholic}}
        </v-btn>

        <v-spacer></v-spacer>

        <v-btn :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'" @click="show = !show"></v-btn>
      </v-card-actions>

      <v-expand-transition>
        <div v-show="show">
          <v-divider></v-divider>

          <v-card-text>
            Category: {{ this.cocktail.strCategory }}
            <br>
            Alcoholic: {{ this.cocktail.strAlcoholic.toLowerCase()=="alcoholic"? "Yes":"No" }}
          </v-card-text>
        </div>
      </v-expand-transition>
    </v-card>
  
</div>
</template>

<script >
import axios from "axios";
  export default{
    name: "drinkCard",
    emits: ['this.cocktail'],
    props: {
      
      cocktailID: Object
    },
    data() {
      return {
        show: false,
        cocktail:null,
        ingredientList:null
      }
    },
    mounted() {
      this.getSpecificCocktail(this.cocktailID);
    }
    ,
    methods: {
      getSpecificCocktail(id) {
        try {
        console.log(id);
        const response = axios.get(`https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i=${id}`).then((response) => {
        this.cocktail = response.data.drinks[0];
        //jesus christ this is ugly
        this.ingredientList = [
          { ingredient: response.data.drinks[0].strIngredient1, measure: response.data.drinks[0].strMeasure1 },

          { ingredient: response.data.drinks[0].strIngredient2, measure: response.data.drinks[0].strMeasure2 },
          { ingredient: response.data.drinks[0].strIngredient3, measure: response.data.drinks[0].strMeasure3 },
          { ingredient: response.data.drinks[0].strIngredient4, measure: response.data.drinks[0].strMeasure4 },
          { ingredient: response.data.drinks[0].strIngredient5, measure: response.data.drinks[0].strMeasure5 },
          { ingredient: response.data.drinks[0].strIngredient6, measure: response.data.drinks[0].strMeasure6 },
          { ingredient: response.data.drinks[0].strIngredient7, measure: response.data.drinks[0].strMeasure7 },
          { ingredient: response.data.drinks[0].strIngredient8, measure: response.data.drinks[0].strMeasure8 },
          { ingredient: response.data.drinks[0].strIngredient9, measure: response.data.drinks[0].strMeasure9 },
          { ingredient: response.data.drinks[0].strIngredient10, measure: response.data.drinks[0].strMeasure10 },
          { ingredient: response.data.drinks[0].strIngredient11, measure: response.data.drinks[0].strMeasure11 },
          { ingredient: response.data.drinks[0].strIngredient12, measure: response.data.drinks[0].strMeasure12 },
          { ingredient: response.data.drinks[0].strIngredient13, measure: response.data.drinks[0].strMeasure13 },
          { ingredient: response.data.drinks[0].strIngredient14, measure: response.data.drinks[0].strMeasure14 },
          { ingredient: response.data.drinks[0].strIngredient15, measure: response.data.drinks[0].strMeasure15 },

        ];
        
      });

      } catch (error) {
        console.error(error);
      }
      }
    }
  }
</script>
