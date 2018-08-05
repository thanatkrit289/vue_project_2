<template>
  <div id="app">
    <HeaderComponent></HeaderComponent>
    <div class="container">
      
      <div class="container">
      
        <div class="row">
          <div class="col">
            <button class="btn btn-success float-right"
              @click="isNewRecipe = !isNewRecipe"
            >Create Recipe</button>
          </div>
        </div>

        <div v-if="isNewRecipe">
          <RecipeForm @formSaved="setRecipeList"></RecipeForm>
        </div>
      </div>  

      <div class="row pt-4">
        <div class="col">
          <h3 class="float-left bold">Search</h3>
          <input type="text" class="form-control" v-model="searchTitle">
        </div>
      </div>

      <div class="row pt-4">
        <div class="col-sm-12 col-md-3"
          v-for="recipe in filterList"
          :key="recipe.id">

          <RecipeCard
            @recipeDeleted="deleteRecipe"
            :recipe="recipe">
          </RecipeCard>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HeaderComponent from './components/HeaderComponent.vue'
import RecipeCard from './components/RecipeCard.vue'
import RecipeForm from './components/RecipeForm.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    HeaderComponent,
    RecipeCard,
    RecipeForm
  },
  data () {
    return {
      isNewRecipe : false,
      recipes: [],
      searchTitle: ''
    }
  },
  methods:{
    setRecipeList (recipe) {
      this.recipes.push(recipe)
      this.isNewRecipe = false
    },
    deleteRecipe(id){
      const index = this.recipes.findIndex((value) => value.id === id)
      this.recipes.splice(index, 1)
      alert('Deleted');
    }
  },
  watch:{
    recipes:{
      handler(){
        // console.log('Recipe Change.')
        console.log("Recipe Change.")
        localStorage.setItem('recipes', JSON.stringify(this.recipes))
      },
      deep: true
    }
  },
  mounted(){
    if(localStorage.getItem('recipes')){
      this.recipes = JSON.parse(localStorage.getItem('recipes'))
      console.log(this.recipes)
    }
  },
  computed:{
    filterList(){
      return this.recipes.filter(recipe => {
        //console.log(recipe.title.toLowerCase().indexOf(this.searchTitle.toLowerCase()) > -1)
        return recipe.title.toLowerCase().indexOf(this.searchTitle.toLowerCase()) > -1
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
