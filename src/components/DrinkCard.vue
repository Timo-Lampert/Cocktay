<template>
  <div v-if="this.cocktail != null" class="wow fadeInUp cardd" data-wow-delay=".5s">
   
    <v-card   class="mx-auto  rounded text-center wavebg  wow fadeInUp " data-wow-delay=".6s" min-height="200px" variant="shaped" max-width="200px">
      
      <a href="#features" @click="this.$emit('cocktailItem', this.cocktail,this.ingredientList)">
      <div class="waves "></div>
      <div class="waves "></div>
      <div class="waves "></div>

          
      <v-img class="cardd"  v-if="this.cocktail.strDrinkThumb != null" lazy-src="\assets\img\hero\images.png" v-bind:src="this.cocktail.strDrinkThumb" width="220px" cover gradient="to bottom, rgba(0,0,0,.0),rgba(20,60,100,.2), rgba(130,150,200,.8)" ></v-img>
      <v-img v-else  src="\assets\img\hero\images.png" height="100%" cover  ></v-img>


      <v-card-title  v-text="this.cocktail.strDrink.toUpperCase().substring(0, 18).trim()"  class="text-dark text-wrap">
      </v-card-title>
 </a>
      <v-card-subtitle class="col-11 col-sm-8 col-md-12 col-xs-4  text-primary">

        {{ this.cocktail.strIngredient1 }}
        ,
        {{ this.cocktail.strIngredient2 }}
        <br>
        {{ this.cocktail.strIngredient3 }}

      </v-card-subtitle>
   
      <v-card-actions>
        <v-btn :color="this.cocktail.strAlcoholic.toLowerCase()=='alcoholic'? 'red':'green'" variant="text">
          {{cocktail.strAlcoholic}}
        </v-btn>

        <v-spacer></v-spacer>

        <v-btn color="dark" :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'" @click="show = !show"></v-btn>
      </v-card-actions>

      <v-expand-transition >
        <div v-show="show">
          <v-divider></v-divider>

          <v-card-text class="text-dark">
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
      cocktailItem: Object,
    },
    data() {
      return {
        show: false,
        cocktail: null,
        ingredientList:null
      }
    },
    mounted() {
      if(this.cocktailItem.strIngredient1 == undefined || this.cocktailItem.strIngredient1 == null){
        
        this.getSpecificCocktail(this.cocktailItem.idDrink);
      }else
      {
        this.cocktail = this.cocktailItem;
        this.setIngredientlist(this.cocktailItem);
      }

    }
    ,
    methods: {
      getSpecificCocktail(id) {
        try {
        console.log(id);
        const response = axios.get(`https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i=${id}`).then((response) => {
        this.cocktail = response.data.drinks[0];
        //jesus christ this is ugly
          this.setIngredientlist(this.cocktail);
        
      });

      } catch (error) {
        console.error(error);
      }
      },
      setIngredientlist(cocktail){
        
        this.ingredientList = [
          { ingredient:  cocktail.strIngredient1, measure: cocktail.strMeasure1 },
          { ingredient:  cocktail.strIngredient2, measure: cocktail.strMeasure2 },
          { ingredient:  cocktail.strIngredient3, measure: cocktail.strMeasure3 },
          { ingredient:  cocktail.strIngredient4, measure: cocktail.strMeasure4 },
          { ingredient:  cocktail.strIngredient5, measure: cocktail.strMeasure5 },
          { ingredient:  cocktail.strIngredient6, measure: cocktail.strMeasure6 },
          { ingredient:  cocktail.strIngredient7, measure: cocktail.strMeasure7 },
          { ingredient:  cocktail.strIngredient8, measure: cocktail.strMeasure8 },
          { ingredient:  cocktail.strIngredient9, measure: cocktail.strMeasure9 },
          { ingredient:  cocktail.strIngredient10, measure: cocktail.strMeasure10 },
          { ingredient:  cocktail.strIngredient11, measure: cocktail.strMeasure11 },
          { ingredient:  cocktail.strIngredient12, measure: cocktail.strMeasure12 },
          { ingredient:  cocktail.strIngredient13, measure: cocktail.strMeasure13 },
          { ingredient:  cocktail.strIngredient14, measure: cocktail.strMeasure14 },
          { ingredient:  cocktail.strIngredient15, measure: cocktail.strMeasure15 },

        ];
      }
    }
  }
</script>
