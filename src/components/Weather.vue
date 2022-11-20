<template>
    <div class="wrapper">
        <div class="title">
           <h1> A Weather App </h1>
        </div>
        <div class="main-card">
            <div v-if="view" class="weather">
                <div class="name">{{name}},{{country}}</div>
                <div class="weather-result">
                    <div>&#127777;{{temperature}}<span>&deg;</span></div>
                    <div>&#127786;{{wind}}<span>km/h</span></div>
                    <div>&#128167;{{humidity}}<span>%</span></div>
                </div>
                <div>{{description}}</div>
            </div>
            <p>{{message}}</p>
            <div class="input">
                <input v-model="city" type="text" placeholder="Enter City name">
                <input @click="loadWeather" type="submit" value="Check">
            </div>
        </div>
        
    </div>
</template>


<script>
import axios from 'axios'


    export default{
        name: 'Weather',
        data(){
            return{
                city:'',
                temperature:'',
                wind:'',
                weather:{},
                view:false,
                humidity:'',
                description:'',
                name:'',
                country:'',
                message:''
            }
        },
        methods:{
            loadWeather(){
                this.view = true
                axios.get("https://api.openweathermap.org/data/2.5/weather?q="+ this.city +"&units=metric&APPID=e341ea7a1c1d81a6fc637d092776acb7")
                .then( response => {
                   this.temperature = response.data.main.temp 
                   this.wind = response.data.wind.speed
                   this.humidity = response.data.main.humidity
                   this.description = response.data.weather[0].description
                   this.name = response.data.name
                   this.country = response.data.sys.country
                   this.city =''
                   this.message = ""

                }).catch((error)=>
                {
                    this.view = false
                    this.message = "Invalid City Input"
                    this.city = ""
                })
            }
        }
    }
</script>

<style scoped>

.wrapper{
    position: relative;
}
.main-card{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: #b7c4cf52;
    border-radius: 25px;
    padding: 2%;
    max-width: 50%;
    margin: auto;
}
.input :first-child{
    border-style: none;
    display: block;
    border-radius: 5px;
    padding: 5px;
    margin-bottom: 10px;
}
.input :last-child{
    border-style: none;
    border-radius: 5px;
    display: block;
    background-color: #967e7672;
    color: #000;
    margin: auto;
    padding: 5px;
    cursor: pointer;
}
.weather{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 2.5px;
    width: fit-content;
    max-height: fit-content;
    color: #fff;
}
.weather-result{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    width: fit-content;
    background:rgba(255, 255, 255, 0.4);
    color: #000;
    padding: 10px;
}
.title{ 
    display: flex;
    justify-content: center; 
    margin-bottom: 2.5%;
    background: #647E68;
    padding: 10px;
    height: fit-content;
    color: #fff
}
.title>h1{
    margin: auto;
    display: inline-block;
}
.name{
    color: #df801a;
    margin: 0 auto;
}

@media only screen and (max-width: 480px){
    .main-card{
        padding: 10px;
        max-width: 70%
    }
    .wrapper{
        width: 100%;
    }
}

</style>