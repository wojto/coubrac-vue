<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12">
                <h1>O Nas</h1>
            </div>
        </div>

        <router-link to="/">Strona główna</router-link>
    </div>
</template>

<script>
    export default {
        name: 'About',
        data()
        {
            return {}
        }
    }
</script>

<style scoped>
    h1 {
        font-weight: normal;
    }
    a {
        color: #42b983;
    }
</style>
