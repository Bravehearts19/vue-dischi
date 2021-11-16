<template>
    <div class="row_container">
        <GenreSelect @onSelectedGenre="onSelectedGenre" :genresList="genresList"/>
        <div class="row row-cols-1 row-cols-md-5 g-4 my-5">
            <div class="col" v-for="(album, i) in filteredAlbumsList" :key="i">
                <AlbumCard :poster="album.poster" :title="album.title" :author="album.author" :genre="album.genre" :year="album.year"></AlbumCard>
            </div>
        </div>
        <Loader v-if="loading === true"></Loader>
    </div>
</template>

<script>
import axios from "axios";
import AlbumCard from './AlbumCard.vue'
import Loader from './Loader.vue';
import GenreSelect from './GenreSelect.vue';

export default {
    name: "AlbumCardContainer",
    components: {
        AlbumCard,
        Loader,
        GenreSelect,
    },
    data() {
        return {
            albumsList: [],
            loading: true,
            activeFilter: "Rock"
        };
    },
    computed: {
        filteredAlbumsList() {
            let filteredAlbumsList = this.albumsList;
            if (this.activeFilter !== "") {
                filteredAlbumsList = this.albumsList.filter((album)=> {
                    return album.genre === this.activeFilter;
                })
            }
            return filteredAlbumsList
        },
        genresList() {
            let genresList = []
            this.albumsList.forEach((album) => {
                if(!genresList.includes(album.genre)) {
                    genresList.push(album.genre)
                }
            });
            return genresList
        }
    },
    methods: {
        fetchData(url) {
            this.loading = true;
            axios.get(url).then((resp) => {
                this.albumsList = resp.data.response;
                setTimeout(() => {
                    this.loading = false;
                }, 1000);
            });
        },
        onSelectedGenre(selectedGenre) {
            this.activeFilter = selectedGenre;
        },
    },
    mounted() {
        this.fetchData("https://flynn.boolean.careers/exercises/api/array/music");
    },
}
</script>

<style lang="scss" scoped>

</style>
