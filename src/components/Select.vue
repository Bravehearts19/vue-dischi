<template>
    <div class="d-flex mt-4 gx-3 px-5">
        <select class="form-select" aria-label="Default select example" @click="selectGenreOption" v-model="selectGenre">
            <option selected value=""></option>
            <option :value="genre" v-for="(genre, i) in genresList" :key="i">{{ genre }}</option>
        </select>

        <select class="form-select" aria-label="Default select example" @click="selectAuthorOption" v-model="selectAuthor">
            <option selected value=""></option>
            <option :value="author" v-for="(author, i) in authorsList" :key="i">{{ author }}</option>
        </select>
    </div>
</template>

<script>
export default {
    name: "Select",
    props: {
        genresList: Array,
        authorsList: Array,
    },
    data() {
        return {
            selectGenre: "",
            selectAuthor: "",
        }
    },
    methods: {
        selectGenreOption() {
            this.$emit("onSelectedGenre", this.selectGenre)
        },
        selectAuthorOption() {
            this.$emit("onSelectedAuthor", this.selectAuthor)
        }
    }
}
</script>

<style>

</style>