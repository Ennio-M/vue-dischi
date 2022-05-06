<template>
    <main>
        <div class="container">
            <app-loader v-if="loading"/>
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
import AppLoader from './AppLoader.vue';
import axios from 'axios';

export default {
    name: 'AppMain',
    components: {
        AppCard,
        AppLoader
    },
    data() {
        return {
            links: [],
            loading: false
        }
    },
    mounted() {
        this.loading = true
        axios.get('https://flynn.boolean.careers/exercises/api/array/music').then((res) => {
            this.links = res.data.response;
        }).catch((error) => {
            console.log(error);
        }).finally(() => {
            this.loading = false;
        })
    }
}
</script>

<style lang="scss" scoped>
    @import '../style/variables.scss';

    main{
        background-color: $bg-dark;
        padding: 50px 0;
        min-height: calc(100% - 82px);
    }
</style>