<template>
    <main>
        <!-- 
        author: "Bon Jovi"
        genre: "Rock"
        poster: "https://www.onstageweb.com/wp-content/uploads/2018/09/bon-jovi-new-jersey.jpg"
        title: "New Jersey"
        year: "1988"
        -->
        <!--
        <div v-for="(item, index) in links" :key="index">
        <img :src="item.poster" :alt="`${item.title} poster`">
        <h4>{{item.title}}</h4>
        <div>{{item.author}}</div>
        <div>{{item.year}}</div>
        </div>
        -->
        <div class="container">
            <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-5 gy-3">
                <div v-for="(item, index) in links" :key="index" class="col">
                    <app-card :album="item"/>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import AppCard from './AppCard.vue';
import axios from 'axios';

export default {
    name: 'AppMain',
    components: {
        AppCard
    },
    data() {
        return {
            links: []
        }
    },
    mounted() {
        axios.get('https://flynn.boolean.careers/exercises/api/array/music').then((res) => {
            this.links = res.data.response;
            console.log(this.links)
        })
    }
}
</script>

<style lang="scss" scoped>
    @import '../style/variables.scss';

    main{
        background-color: $bg-dark;
        padding: 50px 0;
    }
</style>