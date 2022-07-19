<template>
    <main>
        <div class="container">
            <div class="cards-container d-flex align-content-stretch flex-wrap justify-content-between">

                <div class="card" v-for="(album, index) in musicAlbum" :key="index">
                    <img :src="album.poster" class="card-img-top p-3" :alt="album.title">
                    <div class="card-body text-center">
                        <h5 class="text-white fw-bold"> {{album.title}} </h5>
                        <div class="card-text d-flex flex-column">
                            <div>{{album.author}}</div>
                            <div>{{album.year}}</div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </main>
</template>

<script>
import axios from 'axios';

export default {
    data: function(){
        return{
            musicAlbum: [],
        }
    },

    methods:{
        getMusicAlbum(){
            axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then((result) => {
                // console.log(result.data.response)
                this.musicAlbum = result.data.response;
                console.log(this.musicAlbum);
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

        .card{
            width: 180px;
            margin-bottom: 20px;
            background-color: #2e3a46;
            
            .card-body{
                padding: 0 10px 10px 10px;
            }
            .card-text{
                color: #747a7c;
                font-size: 14px;
            }
        }
    }
}
</style>