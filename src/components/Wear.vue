<template>
    <div v-if="wearList.error" class="alert alert-danger">
        {{ wearList.error }}
    </div>
    <div v-else-if="wearList.data">
        <WearNeeded gender={this.props.gender} />
        <WearList />
    </div>
    <div v-else>
        <loader />
    </div>
</template>

<script>
    import Loader from './Loader.vue'
    import { mapMutations } from 'vuex'

    export default {
        name: 'Weather',
        components: { Loader },
        props: {
            location: {
                type: String,
                required: true
            },
            day: {
                type: String,
                required: true
            },
            temperature_scale: {
                type: String,
                required: true
            },
            gender: {
                type: String,
                required: true
            }
        },
        data()
        {
            return {
                api_url: '/api/weather'
            }
        },
        computed: {
            weather: function() {
                return this.$store.state.weather
            },
            renderTemperature() {
                let result = this.weather.temperature;

                if ('f' === this.temperature_scale) {
                    result = this.celciusToFahrenheit(this.weather.temperature);
                }

                return Math.round(result);
            }
        },
        created: function () {
            this.loadWeatherForecastFromServer()
        },
        methods: {
            ...mapMutations([
                'setWeather',
                'setWeatherError'
            ]),
            celciusToFahrenheit(value) {
                return (value * 1.8) + 32;
            },
            loadWeatherForecastFromServer() {
                fetch(this.api_url+'?location='+this.location+'&day='+this.day)
                    .then(response => {
                        return response.json();
                    })
                    .then(data => {
                        if (data.error) {
                            this.$store.commit('setWeatherError', {
                                error: data.error
                            });
                        } else {
                            this.$store.commit('setWeather', {
                                error: false,
                                temperature: data.temperature,
                                humidity: data.humidity,
                                wind: data.wind,
                                rain: data.rain,
                                clouds: data.clouds,
                                icon: data.icon
                            });
                        }
                    })
                    .catch(error => {
                        this.$store.commit('setWeatherError', {
                            error: 'Blad pobierania pogody'
                        });
                    });
            }
        }
    }
</script>

<style scoped>
</style>
