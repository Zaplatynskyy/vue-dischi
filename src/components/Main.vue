<template>
    <main class="debug">
        <div class="container">
            <div v-if="musics.length < 10" class="cont_loader">
                <img src="../assets/img/loader.gif" alt="">
            </div>
            <div v-else class="content_box" v-for="(music, i) in musics" :key="i">
                <Box :music="music"/>
            </div>
        </div>
    </main>
</template>

<script>
import Box from './main_components/Box.vue'
import axios from 'axios'
export default {
    name : 'Main',
    components : {
        Box
    },
    data() {
        return {
            musics : []
        }
    },
    created() {
        axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then((response) => {
                this.musics = response.data.response;
                this.dataLenght = response.data.response.length
            })
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/variables.scss';

    main {
        height: calc(100vh - 70px);
        background-color: $secondary_color;
        overflow: auto;

        .container {
            padding: 20px 0;
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
        }

        .content_box {
            width: calc(100% / 5 - 30px);
            margin: 10px 15px;
        }
        
    }
    
</style>