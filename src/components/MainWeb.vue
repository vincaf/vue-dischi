<template>
    <main>
        <div v-if="isLoading">
            <StartsLoader />
        </div>

        <div v-else class="container">
            <div>
                <SelectGenre :genres="genres" @selectedGenre="filterDiscs" />
            </div>

            <div class="cards-container d-flex align-content-stretch flex-wrap">

                <AlbumMusic v-for="(album, index) in filteredDiscs" :key="index" 
                :imageUrl="album.poster"
                :title="album.title"
                :author="album.author"
                :year="album.year"
                />

            </div>
        </div>
    </main>
</template>

<script>
import AlbumMusic from './AlbumMusic.vue';
import axios from 'axios';
import StartsLoader from './StartsLoader.vue';
import SelectGenre from './SelectGenre.vue';

export default {

    name: 'MainWeb',
    components: {
        AlbumMusic,
        StartsLoader,
        SelectGenre,
    },

    data: function(){
        return{
            musicAlbumList: [],
            genres: [],
            filteredDiscs: [],
            isLoading: true,
        }
    },

    methods:{
        getMusicAlbum(){
            axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then((result) => {
                // console.log(result.data.response)
                this.musicAlbumList = result.data.response;
                console.log(this.musicAlbumList);
                this.filteredDiscs = result.data.response;
                this.genres = this.getUniqueGenres(this.musicAlbumList);
                setTimeout( () => {
                    this.isLoading = false;
                }, 1000);
            })
            .catch((error) => {
                console.warn(error);
            })
        },

        getUniqueGenres(musicAlbumList){
            const genres = [];
            musicAlbumList.forEach(AlbumMusic => {
                if(!genres.includes(AlbumMusic.genre)){
                    genres.push(AlbumMusic.genre);
                }
            });
            return genres;
        },

        filterDiscs(genre){
            if(genre == null || genre === ""){
                this.filteredDiscs = this.musicAlbumList;
            } else{
                this.filteredDiscs = this.musicAlbumList.filter( element => element.genre.toLowerCase() === genre );
            }
        },
    },

    created(){
        this.getMusicAlbum();
    }

}
</script>

<style lang="scss" scoped>
main{
    background-color: #1e2d3b;
    height: 112vh;

    .container{
        max-width: 1000px;

        .cards-container{
            padding: 30px 0;
        }
    }
}
</style>