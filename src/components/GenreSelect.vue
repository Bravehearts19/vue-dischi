<template>
    <select class="form-select" aria-label="Default select example" @click="selectGenreOption" v-model="selectGenre">
        <option selected value=""></option>
        <option :value="genre" v-for="(genre, i) in genresList" :key="i">{{ genre }}</option>
    </select>
</template>

<script>
export default {
    name: "GenreSelect",
    props: {
        genresList: Array,
    },
    data() {
        return {
            selectGenre: "",
        }
    },
    methods: {
        selectGenreOption() {
            this.$emit("onSelectedGenre", this.selectGenre)
        }
    }
}
</script>

<style>

</style>