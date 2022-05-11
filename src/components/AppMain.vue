<template>
    <main>
        <div class="container">
            <app-loader v-if="loading"/>
            <app-search @mySearch="setSearchText" @authorSearch="searchAuthor" :genresList="allGenres" :authorsList="allAuthors"/>
            <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-5 gy-3">
                <div v-for="(item, index) in filteredList" :key="index" class="col">
                    <app-card :album="item"/>
                </div>
            </div>
            <h1 class="text-white py-5" v-if="filteredList.length === 0">Non ci sono album corrispondenti ai criteri selezionati</h1>
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
            allGenres: [],
            allAuthors: [],
            authorValue: ''
        }
    },
    methods: {
        setSearchText(txt) {
            this.searchText = txt;
        },
        searchAuthor(txt) {
            this.authorValue = txt;
        }
    },
    computed: {
        filteredList() {
            return this.links.filter((el) => el.genre.includes(this.searchText) && el.author.includes(this.authorValue));
        }
    },
    mounted() {
        this.loading = true
        axios.get('https://flynn.boolean.careers/exercises/api/array/music').then((res) => {
            this.links = res.data.response;
            this.links.forEach((el) => {
                !this.allGenres.includes(el.genre) ? this.allGenres.push(el.genre) : '';
            });
            this.links.forEach((el) => {
                !this.allAuthors.includes(el.author) ? this.allAuthors.push(el.author) : '';
            });
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