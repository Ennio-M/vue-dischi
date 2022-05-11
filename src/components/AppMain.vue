<template>
    <main>
        <div class="container">
            <app-loader v-if="loading"/>
            <app-search @mySearch="setSearchText" :genresList="allGenres"/>
            <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-5 gy-3">
                <div v-for="(item, index) in filteredList" :key="index" class="col">
                    <app-card :album="item"/>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import AppCard from './AppCard.vue';
import AppLoader from './AppLoader.vue';
import AppSearch from './AppSearch.vue'
import axios from 'axios';

export default {
    name: 'AppMain',
    components: {
        AppCard,
        AppLoader,
        AppSearch
    },
    data() {
        return {
            links: [],
            loading: false,
            searchText: '',
            allGenres: []
        }
    },
    methods: {
        setSearchText(txt) {
            this.searchText = txt;
        }
    },
    computed: {
        filteredList() {
            return this.links.filter((el) => el.genre.includes(this.searchText));
        }
    },
    mounted() {
        this.loading = true
        axios.get('https://flynn.boolean.careers/exercises/api/array/music').then((res) => {
            this.links = res.data.response;
            this.links.forEach((el) => {
                !this.allGenres.includes(el.genre) ? this.allGenres.push(el.genre) : '';
            })
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
        padding-bottom: 50px;
        min-height: calc(100% - 82px);
    }
</style>