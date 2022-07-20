<template>
    <main>
        <div class="container">
            <div class="cards-container d-flex align-content-stretch flex-wrap justify-content-between">

                <AlbumMusic v-for="(album, index) in musicAlbumList" :key="index" 
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

export default {

    name: 'MainWeb',
    components: {
    AlbumMusic,
    },

    data: function(){
        return{
            musicAlbumList: [],
        }
    },

    methods:{
        getMusicAlbum(){
            axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then((result) => {
                // console.log(result.data.response)
                this.musicAlbumList = result.data.response;
                console.log(this.musicAlbumList);
            })
            .catch((error) => {
                console.warn(error);
            })
        }
    },

    created(){
        this.getMusicAlbum();
    }

}
</script>

<style lang="scss" scoped>
main{
    background-color: #1e2d3b;

    .container{
        max-width: 1000px;

        .cards-container{
            padding: 50px 0;
        }
    }
}
</style>