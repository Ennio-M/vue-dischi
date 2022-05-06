<template>
    <div class="card h-100">
        <!-- 
        author: "Bon Jovi"
        genre: "Rock"
        poster: "https://www.onstageweb.com/wp-content/uploads/2018/09/bon-jovi-new-jersey.jpg"
        title: "New Jersey"
        year: "1988"
        -->
        <img :src="album.poster" :alt="`${album.title} poster`" class="card-img-top p-3">
        <div class="card-body text-center">
            <h3 class="card-title text-white text-uppercase fw-bold">{{album.title}}</h3>
            <p class="card-text py-3">
                {{album.author}} <br>
                {{album.year}}
            </p>
        </div>
        
    </div>
</template>

<script>
export default {
    name: 'AppCard',
    props:{
        album: Object
    }   
}
</script>

<style lang="scss" scoped>
    @import '../style/variables.scss';
    .card{
        background-color: $card-bg;
        .card-body{
            padding-top: 0;
            p{
                color: gray;
            }
        }
    }

</style>