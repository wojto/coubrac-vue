<template>
    <div class="spinner-container">
        <div class="spinner">
            <div class="bounce1"></div>
            <div class="bounce2"></div>
            <div class="bounce3"></div>
        </div>
        <div>Wczytywanie...</div>
    </div>
</template>

<script>
    export default {
        name: 'Loader',
        data()
        {
            return {}
        }
    }
</script>

<style scoped>
    .spinner-container {
        width: 100px;
        text-align: center;
        display: inline-block;
    }
    .spinner {
        margin: 10px auto 0;
        width: 70px;
        text-align: center;
    }
    .spinner > div {
        width: 18px;
        height: 18px;
        background-color: #333;
        border-radius: 100%;
        display: inline-block;
        -webkit-animation: sk-bouncedelay 1.4s infinite ease-in-out both;
        animation: sk-bouncedelay 1.4s infinite ease-in-out both;
    }
    .spinner .bounce1 {
        -webkit-animation-delay: -0.32s;
        animation-delay: -0.32s;
    }
    .spinner .bounce2 {
        -webkit-animation-delay: -0.16s;
        animation-delay: -0.16s;
    }
</style>
