<template>
    <div>
        <div class="card" style="width: 18rem;">
            <img class="card-img-top" :src="recipe.image" :alt="recipe.title">
            <div class="card-body">
                <h5 class="card-title">{{recipe.id}} : {{recipe.title}}</h5>
                <p class="card-text">{{recipe.description}}</p>
                <button class="btn btn-danger" @click="sendDelete">Delete</button>
                <button class="btn btn-primary">Go somewhere</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        recipe: {
            type: Object,
            require: true
        }
    },
    methods:{
        sendDelete(){
            this.$emit('recipeDeleted', this.recipe.id)
        }
    }
}
</script>

<style scoped>
</style>