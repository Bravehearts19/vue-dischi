<template>
    <div class="row_container">
        <Select @onSelectedGenre="onSelectedGenre" @onSelectedAuthor="onSelectedAuthor" :genresList="genresList" :authorsList="authorsList"/>
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
import Select from './Select.vue';

export default {
    name: "AlbumCardContainer",
    components: {
        AlbumCard,
        Loader,
        Select,
    },
    data() {
        return {
            albumsList: [],
            loading: true,
            activeGenreFilter: "",
            activeAuthorFilter: "",
        };
    },
    computed: {
        filteredAlbumsList() {
            let filteredAlbumsList = this.albumsList;
            if (this.activeGenreFilter !== "") {
                filteredAlbumsList = this.albumsList.filter((album)=> {
                    return album.genre === this.activeGenreFilter;
                })
            }
            if (this.activeAuthorFilter !== "") {
                filteredAlbumsList = this.albumsList.filter((album)=> {
                    return album.author === this.activeAuthorFilter;
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
        },
        authorsList() {
            let authorsList = []
            this.albumsList.forEach((album) => {
                if(!authorsList.includes(album.author)) {
                    authorsList.push(album.author)
                }
            });
            return authorsList
        },
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
            this.activeGenreFilter = selectedGenre;
        },
        onSelectedAuthor(selectedAuthor) {
            this.activeAuthorFilter = selectedAuthor;
        },
    },
    mounted() {
        this.fetchData("https://flynn.boolean.careers/exercises/api/array/music");
    },
}
</script>

<style lang="scss" scoped>

</style>
