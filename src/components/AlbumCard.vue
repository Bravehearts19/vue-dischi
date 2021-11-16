<template>
    <div class="card">
<!--     <div class="card" v-if="genre !== activeGenre"> -->
        <img class="card-img-top" :src="poster" alt="" />
        <div class="card-body">
            <h5 class="card-title">{{ title }}</h5>
            <div class="card-text">
                <ul>
                    <li>
                        <span class="author_span">{{ author }}</span>
                    </li>

                    <li>
                        <span class="year_span">{{ year }}</span>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: "AlbumCard",
    props: {
        poster: String,
        title: String,
        author: String,
        genre: String,
        year: String,
    },
};
</script>

<style lang="scss" scoped>

</style>