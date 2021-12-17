<template>
    <main>
        <!-- contenitore delle select per filtrare il risultato -->
        <div id="content_select">
            <!-- filtro select per genere -->
            <span>Genere</span>
            <select id="genre" class="select" v-model="selectGenre">
                <option value="">All</option>
                <option :value="genre" v-for="(genre, i) in genres" :key="i">{{genre}}</option>
            </select>

            <!-- filter select per autore -->
            <span>Autore</span>
            <select id="albums" class="select" v-model="selectAuthor">
                <option value="">All</option>
                <option :value="author" v-for="(author, i) in authors" :key="i">{{author}}</option>
            </select>
        </div>

        <!-- container risultato della chiamata filtrato -->
        <div class="container">
            <!-- in attesa di risposta mostra un caricamento -->
            <div v-if="musics.length != responseDataLength" class="cont_loader">
                <img src="../assets/img/loader.gif" alt="">
            </div>
            
            <!-- una volta ottenuto la risposta cicla il risultato e stampa i box degli album -->
            <div v-else class="content_box" v-for="(music, i) in filter" :key="i">
                <!-- componente box al quale passo l'array risultato della chiamata axios -->
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
            musics : [],
            responseDataLength : null,
            genres : [],
            authors : [],
            selectGenre : '',
            selectAuthor : ''

        }
    },

    methods : {
        // funzione per prelevare il genere e gli autori rilevati
        filterX() {
            this.musics.forEach( music => {
                if(!this.genres.includes(music.genre)) {
                    this.genres.push(music.genre);
                    this.genres.sort()
                }

                if(!this.authors.includes(music.author)) {
                    this.authors.push(music.author);
                    this.authors.sort()
                }
            }); 
        }
    },

    created() {
        axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then((response) => {
                this.responseDataLength = response.data.response.length;
                this.musics = response.data.response;
                
                // funzione per prelevare il genere e gli autori rilevati
                this.filterX();
            }
        )        
    },

    computed : {
        // metodo per individuare i box in base ai filtri selezionati
        filter() {
            return this.musics.filter( music => {
                    return music.genre.includes(this.selectGenre) && music.author.includes(this.selectAuthor)
            });
        },
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/variables.scss';

    main {
        height: calc(100vh - 70px);
        background-color: $secondary_color;
        overflow: auto;

        // contenitore delle select per filtrare il risultato
        #content_select {
            text-align: center;
            padding: 20px;

            span {
                font-weight: bold;
                color: $col_white;
                margin-right: 10px;
            }

            .select {
                width: 150px;
                font-size: 16px;
                color: $col_white;
                background-color: $primary_color;
                border: none;
                border-radius: 5px;
                margin-right: 20px;
                padding: 5px;
            }
        }

        // container risultato della chiamata filtrato
        .container {
            padding-bottom: 20px;
            display: flex;
            justify-content: center;
            flex-wrap: wrap;

            .content_box {
                width: calc(100% / 5 - 30px);
                margin: 10px 15px;
            }
        }
    }
    
</style>