<template>
    <div class="d-flex justify-content-center">
        <select class="form-select w-25 mt-4" aria-label="Default select example" v-model="selectedGenre"
        @change="updateSelectedGenre(selectedGenre)">
            <option selected value="">Tutti i generi</option>
            <option v-for="(genre, index) in genres" :key='index' :value="genre.toLowerCase()">
                {{ genre }}
            </option>
        </select>
    </div>
</template>

<script>
export default {
    name: 'SelectGenre',

    props: [
        'genres'
    ],

    data: function(){
        return{
            selectedGenre: "",
        }
    },

    methods: {
        updateSelectedGenre(updatedGenre){
            this.$emit('selectedGenre', updatedGenre);
        }
    }
}
</script>

<style>

</style>