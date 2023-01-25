<script>
export default {
  data() {
    return {
      cocktailName: ''
    }
  },
  methods: {
    search() {
      this.$emit('search', this.cocktailName)
    }
  }
}
</script>



<template>
  <p>
    
  <div>
    <div class="row ">
    <v-text-field elevation='6' :append-inner-icon="'mdi-beer'" class="col-sm-4  wow fadeInUp "  outline v-model="cocktailName" @keyup.enter="search" placeholder="Search for a cocktail" />
    <button @click="search" class="  main-btn align-items-top col-sm-3 border-btn btn-hover wow fadeInUp "
                data-wow-delay=".6s">Search</button>
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
