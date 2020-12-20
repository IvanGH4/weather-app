<template>
    <div :class="typeof weather.main == 'undefined' ? 'wrapper wrapper_def' : typeof weather.main !='undefined' && weather.main.temp > 15 ? 'wrapper wrapper_hot' : 'wrapper wrapper_cold'">
        <div class="search-wrapper">
            <input type="text" placeholder="Search" v-model="city" />
            <button @click="search()"><i class="fas fa-search"></i></button>
        </div>
        <div class="data-wrapper" v-if="typeof weather.main != 'undefined'">
            <h2>{{weather.name}}, {{weather.sys.country}}</h2>
            <h4 class="temp">{{Math.round(weather.main.temp)}} °C</h4>
            <span>{{weather.weather[0].main}}</span>
            <small>{{dateBuilder()}}</small>
        </div>

        <div class="data-wrapper" v-else>
            <h2>Search the weather in your city</h2>
            <h4 class="temp">Degrees °C</h4>
            <span>Weather</span>
            <small>{{dateBuilder()}}</small>
        </div>

        <div class="icons">
            <i :class="typeof weather.main !='undefined' && weather.weather[0].main == 'Clouds' ? 'fas fa-clouds' : 'undefined'"></i>
            <i :class="typeof weather.main !='undefined' && weather.weather[0].main == 'Rain' ? 'fas fa-cloud-showers' : 'undefined'"></i>
            <i :class="typeof weather.main !='undefined' && weather.weather[0].main == 'Clear' ? 'fas fa-sun' : 'undefined'"></i>
            <i :class="typeof weather.main !='undefined' && weather.weather[0].main == 'Mist' ? 'fas fa-fog' : 'undefined'"></i>
        </div>

    
    
        <div class="bottom">
            <h5>
                Weather App
            </h5>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BaseWeather',
    data(){
        return{
            weather: {},
            city: '',
            api_key: '99c7d1c33b51ef03b6c36136f21d4721',
            url_base: 'https://api.openweathermap.org/data/2.5/',
            mainClass: 'wrapper'   
        }
    },
    methods: {
        search(){
            fetch(`${this.url_base}weather?q=${this.city}&units=metric&appid=${this.api_key}`)
            .then(res => {
                return res.json();
            }) .then(this.setResults)
        },
        setResults(results){
            this.weather = results
            console.log(this.weather);
        },
        dateBuilder(){
            let d = new Date();
            let months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
            let days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();

            return `${day} ${date} ${month} ${year}`;
        }
    },
    computed: {
        
    }
}
</script>