<template>
    <div class="loader">
        <img :src="loadingImgUrl" alt="">
        
        <div class="text">Loading albums...</div>
    </div>
</template>

<script>
export default {
    name: "Loader",
    data() {
        return {
            loadingImgUrl: "https://www.pngkey.com/png/full/190-1907956_spotify-logo-png-transparent-spotify-logo-png.png",
        }
    }
};
</script>

<style scoped lang="scss">
@import "@/styles/variables";
.loader {
    position: fixed;
    top: 0;
    left: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    background: $bg-body;
}
img {
    width: 64px;
    margin: 1rem 0;
    animation: pulse 1s infinite alternate;
}
@keyframes pulse {
    from {
        transform: scale(1);
    }
    to {
        transform: scale(1.2);
    }
}
.text {
    text-transform: uppercase;
    letter-spacing: 2px;
    color: white;
}
</style>