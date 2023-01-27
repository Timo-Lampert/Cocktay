
<script>
import axios from 'axios'
import SearchBar from './components/SearchBar.vue'
import CocktailInfo from './components/ItemDescription.vue'
import DrinkCard from './components/DrinkCard.vue'
import { getCurrentInstance } from 'vue';
//axios.defaults.headers.common['X-Api-Key'] = "v1yhUhhqzFYzPX5zWNRkGg==0ftbDzkwtvuaaRyO";
export default {
  components: {
    SearchBar,
    CocktailInfo,
    DrinkCard

  },
  computed: {
    styles: function () {
      return {
        'color': 'rgb(50,150,200)'
      }
    },
  },
  data() {
    return {
      count: 0,
      cocktail: null,
      cocktails: null,
      ingredientList: null,
      partcocktails: null,
      drinkFound: true,
      test: ["a", "b", "c"],
      searchBy: 'filter.php?i=',
      listIndex: 1
    }
  },
  methods: {

    randomCocktail() {
      this.cocktails = [];
      for (let i = 0; i < 3; i++) {


        try {
          const response = axios.get(`https://www.thecocktaildb.com/api/json/v1/1/random.php`).then((response) => {
            this.cocktail = response.data.drinks[0];
            this.ingredientList = null;
            this.cocktails.push(this.cocktail);
            this.listIndex = 1;
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
          this.drinkFound = false;
          console.error(error);
        }
      }
    }
    ,

    getCocktailInfo(cocktailName) {

      const response = axios.get(`https://www.thecocktaildb.com/api/json/v1/1/${this.searchBy}${cocktailName}`).then((response) => {
        this.cocktail = response.data.drinks[0];
        this.cocktails = response.data.drinks;
        this.ingredientList = null;
        this.listIndex = this.listIndex + 1;
        this.listIndex = 1;


        if (response.data.drinks.length > 0) {
          this.drinkFound = true;
        }
        else {
          this.drinkFound = false;
        }


      }).catch((error) => {
        this.cocktails = null
        this.drinkFound = false;
        console.error(error);
      });



    },
    setCocktail(item, ingredientList) {
      this.cocktail = item;
      this.ingredientList = ingredientList;

    }


  }
}
</script>

<template>

  <section id="home" class="hero-section">

    <pagination count="6" />
    <div class="container">
      <div class="row align-items-center position-relative">
        <div class="col-lg-7">
          <div class="hero-content">
            <h2 class="wow fadeInUp" data-wow-delay=".4s">
              Find me a drink!
              <div class="row container">

                <v-radio-group v-model="searchBy" class="col-sm-2  " inline>
                  <v-radio label="Ingredient" value="filter.php?i=" mandatory></v-radio>
                  <v-radio label="Name" value="search.php?s="></v-radio>


                </v-radio-group>

              </div>
              <SearchBar @search="getCocktailInfo" @searchRandom="randomCocktail" />
              <div v-if="!this.drinkFound">
                <h1 class="wow fadeIn " data-wow-delay=".4s">No drink found</h1>
              </div>
            </h2>

            <div class="container">
              <v-container fluid>
      <v-row dense class="">
        <v-col class="wow fadeIn pa-2 " :data-wow-delay="'.'+itemIndex*0.2+'s'"
         v-if="this.cocktails!=undefined && this.cocktails!=null" v-for="(item,itemIndex) in this.cocktails.slice(listIndex * 3 - 3, listIndex * 3)"
          :key="item.idDrink"
          :cols="item.flex"
        >

                  <DrinkCard  :cocktailItem="item" @cocktailItem="setCocktail" 
                    @searchRandom="randomCocktail()" />
                </v-col>
              </v-row>
            </v-container>
            </div>
            <div class="text-center col-l-1 " v-if="this.cocktails != undefined">
              <v-pagination elevation='6' @on-click="listIndex = $event" v-model="listIndex"
                :length="Math.ceil(cocktails.length / 3)" rounded="circle"></v-pagination>

            </div>
          </div>
        </div>

        <div v-if="this.cocktails == null" class="col-lg-3 ">
          <div class="hero-img wow fadeInUp" data-wow-delay=".5s">

            <img src="../assets/img/hero/hero-img.jpg" alt=""
              v-if="this.cocktails == undefined || this.cocktails.length < 4" class="heroimg d-none d-lg-block"
              height="600" style="border-radius:50px" />
            <img src="../assets/img/hero/hero-img.jpg" class="hero-img wow fadeInUp d-none d-md-block" v-else
              height="600" style="border-radius:50px" />

          </div>
        </div>
      </div>
    </div>


  </section>

  <!-- ======== feature-section start ======== -->
  <section id="features" class="feature-section pt-120">
    <div class="container" v-if="!cocktail">
      <div class="row justify-content-center">
        <div class="col-lg-4 col-md-8 col-sm-10">

          <div class="single-feature col-sm-8">
            <div class="icon">
              <font-awesome-icon icon="fa-solid fa-magnifying-glass " />
            </div>
            <div class="content ">
              <h1> Choose a drink first!</h1>

            </div>
          </div>
        </div>
      </div>
    </div>

    <CocktailInfo v-if="cocktail" :cocktail="cocktail" :ingredientList="ingredientList" />

  </section>
  <!-- ======== feature-section end ======== -->

</template>

