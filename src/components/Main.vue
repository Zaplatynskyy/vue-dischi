<template>
    <main class="debug">
        <div class="container">
            <div class="content_box" v-for="(music, i) in musics" :key="i">
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
@import '../assets/style/variables.scss';

    main {
        height: calc(100vh - 70px);
        background-color: $secondary_color;
        overflow: auto;

        .container {
            padding: 20px 0;
            display: flex;
            flex-wrap: wrap;
        }

        .content_box {
            width: calc(100% / 5 - 30px);
            margin: 10px 15px;
        }
        
    }
    
</style>