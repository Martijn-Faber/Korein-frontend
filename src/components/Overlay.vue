<template>
    <div v-if="overlayActive">
        <div class="overlay">
            <img src="../assets/korein-logo.svg" alt="logo" class="overlay-logo">
            <div class="shape"></div>
            <h1 class="overlay-text">3</h1>
        </div>
    </div>
</template>

<script>
export default {
    name: "Overlay",
    props: {
        overlayActive: Boolean
    }
}
</script>

<style scoped>
.overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #fff;
    width: 100vw;
    height: 100vh;
}

.overlay-text {
    position: absolute;
    transform: translate(-50%, -100%);
    top: 50%;
    left: 50%;
    transition: all 0.3s;

    font-size: 400px;
    font-weight: 200;
}

.shape {
    background-color: #0086eb;
    position: absolute;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    width: 500px;
    height: 500px;
    border-radius: 37% 63% 65% 35% / 59% 38% 62% 41%;
    transition: all 0.3s;
}
</style>