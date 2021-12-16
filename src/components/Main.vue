<template>
    <main class="debug">
        <div class="container py-5">
            <div class="row gy-3">
                <div class="col" v-for="(music, i) in musics" :key="i">
                    <div class="box">
                        <img src="https://www.onstageweb.com/wp-content/uploads/2018/09/bon-jovi-new-jersey.jpg" alt="">

                        <h2>New Jersey</h2>
                        
                        <div class="name">Bon Jovi</div>
                        <div class="year">1988</div>
                    </div>
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
                this.musics = response.data.response
            })
    }
}
</script>

<style lang="scss" scoped>
@import '../../node_modules/bootstrap/scss/bootstrap-grid.scss';
    main {
        height: calc(100vh - 70px);
        background-color: #1e2d3b;
        overflow: auto;
    }

    // DEBUG
    .debug .box {
        width: 200px;
        height: 300px;
        text-align: center;
        background-color: red;
        padding: 10px;

        img {
            width: 100%;       }
    }
    
</style>