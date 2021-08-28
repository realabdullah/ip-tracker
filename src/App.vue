<template>
<div class="header">
    <h2>IP Address Tracker</h2>
    <div class="input">
      <input type="text" placeholder="Search for any IP address or domain">
      <p @click="findIt">
        <img src="./assets/images/icon-arrow.svg" alt="icon">
      </p>
    </div>

    <div class="modal" id="modal">
      <span>Ip Address</span>
      <p>{{ resultData.ip }}</p>

      <span>Location</span>
      <p>{{ resultData.location }}</p>

      <span>Timezone</span>
      <p>{{ resultData.timezone }}</p>

      <span>Isp</span>
      <p>{{ resultData.isp }}</p>
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
    const ipResult = ref([])
    const resultData = reactive({
      ip: '',
      location: '',
      timezone: '',
      isp: ''
    })

    const findIt = async () => {
      axios.get('https://geo.ipify.org/api/v1?apiKey=at_lh7Y3Y5INgArPaCYvbp8IflKq6nDp&ipAddress=8.8.8.8')
      .then(response => {
        ipResult.value = response.data
        resultData.ip = ipResult.value.ip
        resultData.location = ipResult.value.location.country
        resultData.timezone = ipResult.value.location.timezone
        resultData.isp = ipResult.value.isp
        console.log(resultData.ip)
        document.getElementById('modal').style.display = 'block'
      })
      .catch(error => {
        console.log(error)
      })
    }

    return {
      findIt,
      resultData
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
img {
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
.map-area {
  min-height: 50vh;
  background: url('./assets/images/map.jpg');
  background-size: cover;
  background-repeat: no-repeat;
}
</style>
