<template>
  <div class="header">
    <h2>IP Address Tracker</h2>
    <div class="input">
      <input type="text" v-model="searchip" placeholder="Search for any IP address or domain">
      <a href="#modal" role="button" >
        <img src="../assets/images/icon-arrow.svg" alt="icon">
      </a>
    </div>

    <div class="modal" id="modal">
      <span>Ip Address</span>
      <p>Oops!</p>

      <span>Location</span>
      <p>I'm not</p>

      <span>Timezone</span>
      <p>Functional yet!</p>

      <span>Isp</span>
      <p>Check Back later</p>
      <a href="#!" class="outside-trigger"></a>
    </div>
  </div>
  <div class="map-area">

  </div>
</template>

<script>
export default {
  name: 'Tracker',
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  background-image: url('../assets/images/pattern-bg.png');
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
a {
  text-decoration: none;
  margin-top: 5px;
}
img {
  background: #000;
  padding: 16px;
  border-radius: 0 8px 8px 0;
}
.modal {
  position: absolute;
  top: 150px;
  left: 0;
  right: 0;
  margin: 20px;
  padding: 30px;
  background: #fff;
  border-radius: 10px;
}
#modal {
	opacity: 0;
	transition: .5s ease-in-out;
	visibility: hidden;
}
#modal:target {
  opacity: 1;
  visibility: visible;
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
.outside-trigger {
	bottom: 0;
	cursor: default;
	left: 0;
	position: fixed;
	right: 0;
	top: 0;
}
.map-area {
  min-height: 50vh;
  background: url('../assets/images/map.jpg');
  background-size: cover;
  background-repeat: no-repeat;
}
</style>
