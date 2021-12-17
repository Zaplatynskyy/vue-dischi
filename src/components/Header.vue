<template>
    <header>
        <!-- logo pagina -->
        <img src="../assets/img/logo.png" alt="">
    </header>
</template>

<script>
export default {
    name : 'Header'
}
</script>

<style lang="scss" scoped>
@import '../assets/style/variables.scss';

    header {
        height: 70px;
        background-color: $primary_color;

        // logo pagina
        img {
            height: 100%;
            padding: 10px;
        }
    }
</style>