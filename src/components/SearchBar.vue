<script>
export default {
  data() {
    return {
      cocktailName: ''
    }
  },
  methods: {
    searchRandom() {
      this.$emit('searchRandom')
    },
    search() {
      this.$emit('search', this.cocktailName)
    }
  }
}
</script>



<template>
  <p>

  <div>

    <div class="row justify-content-between">
      <v-text-field elevation='6' :append-inner-icon="'mdi-beer'" class="col-sm-4 wow fadeInUp  " outline
        v-model="cocktailName" @keyup.enter="search" placeholder="Search for a cocktail" />
      <button @click="search" style="translate:0 -10px 0;"
        class="  main-btn   col-sm-3 border-btn btn-hover wow fadeInUp p-2  align-items-stretch"
        data-wow-delay=".6s">Search</button>
      <div class="col-sm-1 center-text"></div>
      <button style="border-radius: 50px;translate:0 -10px 0; border-style:dashed;" @click="searchRandom()"
        class="  main-btn   col-sm-1 border-btn btn-hover btn-outline-dark wow fadeInUp p-2 p  align-items-stretch "
        data-wow-delay=".6s" :append-inner-icon="'mdi-beer'"> <font-awesome-icon icon="fa-solid fa-random" /></button>
    </div>
  </div>
  </p>
</template>

<style scoped>
input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 20px;
  box-sizing: border-box;
  margin-top: 6px;
  margin-bottom: 16px;

  resize: vertical;
}

.error {
  color: red;
}
</style>
