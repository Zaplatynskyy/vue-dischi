<template>
    <main class="debug">
        <div class="container py-5">
            <div class="row">
                <div class="col-12">
                    <div class="box"></div>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import axios from 'axios'
export default {
    name : 'Main',
    data() {
        return {
            musics : null
        }
    },
    created() {
        axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then((response) => {
                this.musics = response.data
            })
    }
}
</script>

<style lang="scss" scoped>
@import '../../node_modules/bootstrap/scss/bootstrap-grid.scss';
    main {
        height: calc(100vh - 70px);
        background-color: #1e2d3b;
    }

    // DEBUG
    .debug .box {
        width: 200px;
        height: 300px;
        background-color: red;
    }
    
</style>