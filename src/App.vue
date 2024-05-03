<template>
  <div className="wrapper">
   <h1 className="header">Weather today</h1>
   <p>Find out the weather in the {{ city=="" ? "city": cityName }}</p>
   <input type="text" v-model="city" placeholder="Enter the city">
   <button v-if ="city !=''" @click="getWeather()">Get the weather</button>
   <button v-else disabled>Enter the city</button>
   <p className="error">{{ error }}</p>
 
 <div v-if="info != null">
   <p>{{ showTemp }}</p>
   <p>{{ showFeelsLike }}</p>
   <p>{{ showMinTemp }}</p>
   <p>{{ showMaxTemp }}</p>
 </div>
   
  </div>
 </template>
 
 <script>
 import axios from 'axios'
 export default{
 data(){
   return{
     city: "",
     error: "",
     info: null
   }
 },
 computed: {
   cityName(){
     return "«" + this.city + "»"
     },
     showTemp(){
       return "Temperature: " + this.info.main.temp
     },
     showFeelsLike(){
       return "Feels like: " + this.info.main.feels_like
     },
     showMinTemp(){
       return "Min temperature: " + this.info.main.temp_min
     },
     showMaxTemp(){
       return "Max temperature: " + this.info.main.temp_max
     },
 
 },
 methods: {
   getWeather(){
 if(this.city.trim().length < 2){
 this.error = "Enter more than one character"
   return false
   
 }
 this.error = ""
 
 axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=d2615434e78ad5450f5cb0409e0e4c6d`)
 .then(res => (this.info = res.data))  
 }
 }
 }
 </script>
 
 <style scoped>
 
 .error{
   color: #d03939;
 }
 
 .wrapper{
   width: 900px;
   height: 500px;
   border-radius: 50px;
   background: #1f0f24;
   text-align: center;
   color: #fff;
   padding-top: 50px;
 }
 
 .wrapper h1{
   margin-top: 20px;
 }
 
 .wrapper p{
   margin-top: 20px;
 }
 
 .wrapper input{
   margin-top: 30px;
   background: transparent;
   border: 0;
   border-bottom: 2px solid #110813;
   color: #fcfcfc;
   font-size: 16px;
   padding: 5px 8px;
   outline: none;
 }
 
 .wrapper input:focus{
   border-bottom-color: #6e2d7d;
 }
 
 .wrapper button{
   background: #e3bc4b;
   color: #fff;
   border-radius: 10px;
   border: 2px solid #b99935;
   padding: 10px 15px;
   margin-left: 20px;
   cursor: pointer;
   transition: transform 500ms ease;
 
 }
 
 .wrapper button:disabled{
   background: #746027;
   cursor: not-allowed;
 }
 
 .wrapper button:hover{
   transform: scale(1.1) translateY(-5px);
 }
 </style>
 