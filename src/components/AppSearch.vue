<template>
    <div>
        <div class="input-group py-3">
            <p class="text-white m-0">Seleziona un genere</p>
            <select name="genres" id="genres" v-model="inputText" @change="search" class="mx-3 p-2 rounded-3">
                <option value="">Tutti</option>
                <option :value="genre" v-for="(genre, index) in genresList" :key="index">{{genre}}</option>
            </select>
            <p class="text-white m-0">Seleziona un artista</p>
            <select name="authors" id="authors" v-model="inputAuthor" @change="searchAuthor" class="mx-3 p-2 rounded-3">
                <option value="">Tutti</option>
                <option :value="author" v-for="(author, index) in authorsList" :key="index">{{author}}</option>
            </select>
        </div>
    </div>
</template>

<script>
export default {
    name: 'AppSearch',
    data() {
        return {
            inputText: '',
            inputAuthor: ''
        }
    },
    props: {
        genresList: Array,
        authorsList: Array
    },
    methods: {
        search() {
            this.$emit('mySearch', this.inputText);
        },
        searchAuthor() {
            this.$emit('authorSearch', this.inputAuthor);
        }
    }
}
</script>

<style lang="scss" scoped>
    p{
        line-height: 37px;
        font-size: 1.2em;
    }
    select{
        font-size: 1.2em;
    }
</style>