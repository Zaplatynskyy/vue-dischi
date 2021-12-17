<template>
    <div class="box">
        <!-- immagine album -->
        <img :src="music.poster" :alt="music.author">

        <!-- titolo album -->
        <h3>{{music.title}}</h3>
        
        <!-- nome autore e anno uscita album -->
        <div class="name">{{music.author}}</div>
        <div class="year">{{music.year}}</div>
    </div>
</template>

<script>
export default {
    name : 'Box',
    props : {
        music : Object
    }
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/variables.scss';

    .box {
        height: 100%;
        text-align: center;
        background-color: $primary_color;
        padding: 20px;

        img {
            width: 100%;       
        }

        h3 {
            color: $col_white;
            text-transform: uppercase;
            margin: 15px 0;
        }

        .name, .year {
            color : $col_text;
        }

        .year {
            margin-bottom : 30px
        }
    }
</style>