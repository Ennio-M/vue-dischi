<template>
    <header>
        <img src="../assets/imgs/logo.png" alt="Logo Spotify" class="my-3 mx-4">
    </header>
</template>

<script>
export default {
    name: 'AppHeader'
}
</script>

<style lang="scss" scoped>
    @import '../style/variables.scss';
    header{
        background-color: $card-bg;
        img{
            width: 50px;
        }
    }
</style>