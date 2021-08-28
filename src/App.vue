<template>
<div class="header">
    <h2>IP Address Tracker</h2>
    <div class="input">
      <input type="text" v-model="myIp" placeholder="Search for any IP address or domain">
      <p @click="findIt">
        <img class="arrow" src="./assets/images/icon-arrow.svg" alt="icon">
      </p>
    </div>

    <div class="modal" id="modal">
      <div class="resultsec" v-if="!loading">
        <div>
          <span>Ip Address</span>
          <p>{{ resultData.ip }}</p>
        </div>
        
        <div class="line"></div>

        <div>
          <span>Location</span>
          <p>{{ resultData.city + ', ' + resultData.region + ', ' + resultData.location }}</p>
        </div>
        
        <div class="line"></div>

        <div>
          <span>Timezone</span>
          <p>{{ resultData.timezone }}</p>
        </div>
        
        <div class="line"></div>

        <div>
          <span>Isp</span>
          <p>{{ resultData.isp }}</p>
        </div>
        
        <div @click="close" class="close">
          close
        </div>
      </div>
      <div v-else>
        <img :src="loadingImage"/>
      </div>
    </div>
  </div>
  <div class="map-area">

  </div>
</template>

<script>
import axios from 'axios'
import { ref, reactive } from 'vue'

export default {
  setup() {
    const myIp = ref('')
    const abd = myIp.value
    const ipResult = ref([])
    const loading = ref(true)
    const loadingImage = require('./assets/load.svg')

    const resultData = reactive({
      ip: '',
      location: '',
      city: '',
      region: '',
      timezone: '',
      isp: ''
    })

    const findIt = async () => {
      document.getElementById('modal').style.display = 'block'
      var api_key = 'at_lh7Y3Y5INgArPaCYvbp8IflKq6nDp';
      var api_url = 'https://geo.ipify.org/api/v1?';
      var url = api_url + 'apiKey=' + api_key + '&ipAddress=' + myIp.value;
      axios.get(url)
      .then(response => {
        ipResult.value = response.data
        resultData.ip = ipResult.value.ip
        resultData.location = ipResult.value.location.country
        resultData.city = ipResult.value.location.city
        resultData.region = ipResult.value.location.region
        resultData.timezone = ipResult.value.location.timezone
        resultData.isp = ipResult.value.as.name
        console.log(ipResult.value)
        loading.value = false
        myIp.value = ''
      })
      .catch(error => {
        console.log(error)
      })
    }

    const close = () => {
      document.getElementById('modal').style.display = 'none'
    }

    return {
      myIp,
      findIt,
      resultData,
      close,
      abd,
      loading,
      loadingImage
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Rubik', sans-serif;
}
.header {
  background-image: url('./assets/images/pattern-bg.png');
  background-size: cover;
  background-repeat: no-repeat;
  padding: 30px 20px;
  text-align: center;
  position: relative;
  min-height: 350px;
}
.header h2 {
  color: #fff;
  margin: 25px auto;
}
.input {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}
input {
  padding: 15px;
  border: none;
  width: 100%;
  border-radius: 8px 0 0 8px;
}
input::placeholder {
  color: hsl(0, 0%, 17%);
  font-weight: bold;
}
p {
  text-decoration: none;
  margin-top: 5px;
}
.arrow {
  background: #000;
  padding: 16px;
  border-radius: 0 8px 8px 0;
}
.modal {
  display: none;
  position: absolute;
  top: 150px;
  left: 0;
  right: 0;
  margin: 20px;
  padding: 30px;
  background: #fff;
  border-radius: 10px;
}
.modal span {
  text-transform: uppercase;
  font-size: 10px;
  font-weight: 500;
  padding: 10px;
  color: hsl(0, 1%, 41%);
}
.modal p {
  margin: 10px auto;
  margin-bottom: 20px;
  font-weight: 500;
  font-size: 18px;
}
.close {
  cursor: pointer;
  padding: 10px;
  border: 2px solid #4f5abc;
  font-weight: bold;
  width: 70px;
  color: #4f5abc;
}

.map-area {
  min-height: 50vh;
  background: url('./assets/images/map.jpg');
  background-size: cover;
  background-repeat: no-repeat;
}
@media(min-width: 800px) {
  .input {
    width: 80%;
    margin: auto;
  }
  .resultsec {
    display: flex;
    align-items: center;
    justify-content: space-between;
    text-align: left;
  }
  .line {
    width: 1.5px;
    height: 58px;
    margin: 10px;
    background-color: hsl(0, 1%, 41%);
  }
  .close {
    display: none;
  }
}
</style>
