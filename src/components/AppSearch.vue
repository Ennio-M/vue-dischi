<template>
    <div>
        <div class="input-group py-3">
            <p class="text-white m-0">Seleziona un genere</p>
            <select name="genres" id="genres" v-model="inputText" @change="search" class="mx-3 p-2 rounded-3">
                <option value="">Tutti</option>
                <option :value="genre" v-for="(genre, index) in genresList" :key="index">{{genre}}</option>
            </select>
        </div>
    </div>
</template>

<script>
export default {
    name: 'AppSearch',
    data() {
        return {
            inputText: ''
        }
    },
    props: {
        genresList: Array
    },
    methods: {
        search() {
            this.$emit('mySearch', this.inputText);
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