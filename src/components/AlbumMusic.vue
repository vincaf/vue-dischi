<template>
    <div class="card">
        <img :src="imageUrl" class="card-img-top p-3" :alt="title">
        <div class="card-body text-center">
            <h5 class="text-white fw-bold text-uppercase"> {{title}} </h5>
            <div class="card-text d-flex flex-column">
                <div>{{author}}</div>
                <div>{{year}}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {

    props:{
        'imageUrl': String,
        'title': String,
        'author': String,
        'year': Number,
    }

}
</script>

<style lang="scss" scoped>
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
</style>