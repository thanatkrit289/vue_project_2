<template>
    <div>
        <form @submit.prevent="save">
            <div class="form-group">
                <label for="Title">Title</label>
                <input type="text" class="form-control" id="" placeholder="Title"
                    v-model="recipe.title"
                >
            </div>

            <div class="form-group">
                <label for="Description">Description</label>
                <input type="text" class="form-control" id="" placeholder="Description"
                    v-model="recipe.description"
                >
            </div>

            <div class="form-group">
                <label for="Image">Image</label>
                <input type="text" class="form-control" id="" placeholder="Image URL"
                    v-model="recipe.image"
                >
            </div>

            {{recipe}}
            <button type="reset" class="btn btn-danger">CANCEL</button>
            <button type="submit" class="btn btn-primary">SAVE</button>
        </form>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                recipe:{
                    id: '',
                    title: '',
                    description: '',
                    image: ''
                }
            }
        },
        methods: {
            save() {
                this.recipe.id = Math.random().toString(36).substring(7)
                this.$emit('formSaved', this.recipe)
            }
        }
    }
</script>

<style scoped>

</style>