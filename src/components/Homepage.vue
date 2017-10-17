<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12">
                <h1>Co dziś ubrać?</h1>
            </div>
        </div>

        <options-form :gender="params.gender" :temperature_scale="params.temperature_scale"
                      :location="params.location"/>

        <router-link to="about">O nas / kontakt</router-link>
    </div>
</template>

<script>
    import OptionsForm from './OptionsForm.vue'
    export default {
        name: 'Homepage',
        components: { OptionsForm },
        data()
        {
            return {
                params: {
                    gender: 'f',
                    temperature_scale: 'c',
                    location: 'Warszawa'
                }
            }
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
