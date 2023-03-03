@import './main.css';

<script>
export default {
 data() {
   return {
     city: '',
     region: '',
     country: '',
     longitude: '',
     latitude: '',
     weather: '',
     temp: '',
     humidity: '',
     NY: '',
     SG: '',
     Mumbai: '',
     Delhi: '',
     Sydney: '',
     Melbourne: '',
     NYTemp: '',
     SGTemp: '',
     MumbaiTemp: '',
     DelhiTemp: '',
     SydneyTemp: '',
     MelbourneTemp: ''
   }
 },

 testLog() {
   console.log('in testLog')
 },
 
 methods: {
   async getGeolocationInformation() {
     const API_KEY = 'a38b61fe26ef4d799783306ba4aea923';
     const API_URL = 'https://ipgeolocation.abstractapi.com/v1/?api_key=' + API_KEY;
     try {
       this.errorMessage = '';
       const apiResponse = await fetch(API_URL);
       const data = await apiResponse.json();
       const {city, country, region, longitude, latitude} = data;
       this.city = city;
       this.region = region;
       this.country = country;
       this.longitude = longitude;
       this.latitude = latitude;
     } catch (error) {
       this.errorMessage = error.message;
     }
   },
   async checkLoc() {
     this.longitude = this.longitude.trim().toString();
     this.latitude = this.latitude.trim().toString();
   },
   async getWeatherInformation() {
     await this.getGeolocationInformation();
     const API_KEY_2 = '1abbb4f40d3ebce35e5b8e2f6b7460c5';
     const API_URL_2 = 'https://api.openweathermap.org/data/2.5/weather?lat=' + this.latitude 
+ '&lon=' + this.longitude + '&appid=' + API_KEY_2 + '&units=metric';
     const API_URL_3 = 'https://api.openweathermap.org/data/2.5/weather?q='
     console.log('latitide: ' + this.latitude);
     try {
       this.errorMessage = '';
       const apiResponse2 = await fetch(API_URL_2);
       const data2 = await apiResponse2.json();
       const {weather, main} = data2;
       this.weather = weather[0]['main'];
       this.temp = main['temp'];
       this.humidity = main['humidity'];

       const apiResponse3 = await fetch(API_URL_3 + 'New York'+ '&appid=' + API_KEY_2 + '&units=metric');
       const data3 = await apiResponse3.json();
       this.NY = data3['weather'][0]['main'];
       this.NYTemp = data3['main']['temp'];

       const apiResponse4 = await fetch(API_URL_3 + 'Singapore'+ '&appid=' + API_KEY_2 + '&units=metric');
       const data4 = await apiResponse4.json();
       this.SG = data4['weather'][0]['main'];
       this.SGTemp = data4['main']['temp'];

       const apiResponse5 = await fetch(API_URL_3 + 'Mumbai'+ '&appid=' + API_KEY_2 + '&units=metric');
       const data5 = await apiResponse5.json();
       this.Mumbai = data5['weather'][0]['main'];
       this.MumbaiTemp = data5['main']['temp'];

       const apiResponse6 = await fetch(API_URL_3 + 'Singapore'+ '&appid=' + API_KEY_2 + '&units=metric');
       const data6 = await apiResponse6.json();
       this.Delhi = data6['weather'][0]['main'];
       this.DelhiTemp = data6['main']['temp'];

       const apiResponse7 = await fetch(API_URL_3 + 'Singapore'+ '&appid=' + API_KEY_2 + '&units=metric');
       const data7 = await apiResponse7.json();
       this.Sydney = data7['weather'][0]['main'];
       this.SydneyTemp = data7['main']['temp'];

       const apiResponse8 = await fetch(API_URL_3 + 'Singapore'+ '&appid=' + API_KEY_2 + '&units=metric');
       const data8 = await apiResponse8.json();
       this.Melbourne = data8['weather'][0]['main'];
       this.MelbourneTemp = data8['main']['temp'];
     } catch (error) {
       this.errorMessage = error.message;
     }
   }
 },

 mounted() {
   this.getWeatherInformation();
 }
}
</script>

<template>
  <div class = "row">
    <h2>Welcome!</h2>
    <p> Your current location is: {{ city }} in {{region}}, {{country}}, {{latitude}}, {{longitude}}. </p>
    <p> The current weather condition at your location is: {{weather}}, with temperatures of {{temp}}°C, and humidity of {{humidity}}%. </p>
    <p :style="{color: 'red'}">{{errorMessage}}</p>
  </div>

  <div>
    <figure>
      <img src="./assets/newyork.webp" alt="Mountains">
      <figcaption>
        <p>{{NY}}</p>
        Newyork, {{NYTemp}}°C
      </figcaption>
    </figure>
    <figure>
      <img src="./assets/singapore.jpeg" alt="Mountains">
      <figcaption>
        <p>{{SG}}</p>
        Singapore, {{SGTemp}}°C
      </figcaption>
    </figure>
    <figure>
      <img src="./assets/mumbai.jpeg" alt="Mountains">
      <figcaption>
        <p>{{Mumbai}}</p>
        Mumbai, {{MumbaiTemp}}°C
      </figcaption>
    </figure>
    <figure>
      <img src="./assets/delhi.jpeg" alt="Mountains">
      <figcaption>
        <p>{{Delhi}}</p>
        Delhi, {{DelhiTemp}}°C
      </figcaption>
    </figure>
    <figure>
      <img src="./assets/sydney.jpeg" alt="Mountains">
      <figcaption>
        <p>{{Sydney}}</p>
        Sydney, {{SydneyTemp}}°C
      </figcaption>
    </figure>
    <figure>
      <img src="./assets/melbourne.jpeg" alt="Mountains">
      <figcaption>
        <p>{{Melbourne}}</p>
        Melbourne, {{MelbourneTemp}}°C
      </figcaption>
    </figure>
  </div>
</template>

