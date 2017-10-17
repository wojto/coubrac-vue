<template>
    <div>
        <div class="row">
            <div class="col-md-12">
                <form method="get" @submit="handleSubmit">
                    Co&nbsp;
                    <select-editable :options="gender_options" :selected="gender"
                                     v-on:handleChange="handleGenderChange" />
                        &nbsp;<span v-if="gender == 'f'">powinna</span><span v-else>powinien</span>&nbsp;
                    <select-editable :options="day_options" :selected="day" v-on:handleChange="handleDayChange" />
                    &nbsp;ubrać w lokalizacji&nbsp;
                    <input-editable v-on:handleChange="handleLocationChange" :value="location"/>
                    <br/>
                    Pokaż pogodę w:&nbsp;
                    <select-editable :options="temperature_scale_options" :selected="temperature_scale"
                                     v-on:handleChange="handleTemperatureScaleChange" />
                </form>
            </div>
        </div>

        <weather :location="location" :day="day" :temperature_scale="temperature_scale" :gender="gender"/>
    </div>
</template>

<script>
    import SelectEditable from './SelectEditable.vue'
    import InputEditable from './InputEditable.vue'
    import Weather from './Weather.vue'
    export default {
        name: 'Homepages',
        components: { SelectEditable, InputEditable, Weather },
        data()
        {
            return {
                gender: 'f',
                location: 'Warszawa',
                temperature_scale: 'c',
                day: '0',
                gender_options: [{value: 'f', name: 'kobieta'}, {value : 'm', name: 'mężczyzna'}],
                day_options: [{value: '0', name: 'dziś'}, {value : '1', name: 'jutro'}, {value : '2',
                    name: 'pojutrze'}],
                temperature_scale_options: [{value: 'c', name: '°C'}, {value : 'f', name: '°F'}]
            }
        },
        methods: {
            handleSubmit (event) {
                event.preventDefault();
            },
            handleGenderChange(value) {
                this.gender = value;
            },
            handleDayChange(value) {
                this.day = value;
            },
            handleTemperatureScaleChange(value) {
                this.temperature_scale = value;
            },
            handleLocationChange(value) {
                this.location = value;
            }
        }
    }
</script>

<style scoped>
</style>
