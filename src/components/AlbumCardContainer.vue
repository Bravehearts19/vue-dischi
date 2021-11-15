<template>
    <div>
        <div class="row row-cols-1 row-cols-md-5 g-4 my-5">
            <div class="col" v-for="(album, i) in albumsList" :key="i">
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

export default {
    name: "AlbumCardContainer",
    components: {
        AlbumCard,
        Loader,
    },
    data() {
        return {
            albumsList: [],
            loading: true,
        };
    },
    methods: {
        fetchData(url) {
            this.loading = true;
            axios.get(url).then((resp) => {
                this.albumsList = resp.data.response;
                setTimeout(() => {
                    this.loading = false;
                }, 6000);
            });
        },
    },
    mounted() {
        this.fetchData("https://flynn.boolean.careers/exercises/api/array/music");
    },
}
</script>

<style lang="scss" scoped>

</style>
