<template>
    <header>
        <img :src="spotifyImgUrl" alt="">
    </header>
</template>

<script>
export default {
    name: "Header",
    data() {
        return {
            spotifyImgUrl: "https://www.pngkey.com/png/full/190-1907956_spotify-logo-png-transparent-spotify-logo-png.png",
        }
    }
}
</script>